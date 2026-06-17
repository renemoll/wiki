---
title: Lock free queue
description: 
published: true
date: 2026-06-17T20:48:26.064Z
tags: 
editor: markdown
dateCreated: 2025-08-28T19:25:03.156Z
---

# Single producer single consumer queue

For my embedded applications, I need to transfer data from inside interupt context to another context quickly. A good solution for this is to use a single producer single consumer (SPSC) queue.

Now, there are already quite a few implementation available, yet I wanted to go through the design and constraint choises and understand their implact. This document documents my journey. 

First, we go through my needs which form the requirements for the queue. Next, I walk you through various design options and which choises I made. 
> TODO: finally

## Requirements

Now, I want simple FIFO behaviour for this queue: `push` to add the newest data element to the queue and `pop` to remove the oldest. The next sections elaborate the queue's behaviour.

### Target machine

I primairily aim for ARM Cortex-M based microcontrollers, specifically the Cortex-M4/M7/M33 families.

These microcontrollers feature:
* 32-bit architecture with 32-bit atomic operations;
* optional data cache;
* optional tichtly coupled memory (TCM);

Besides microcontrollers, the implementation must be compatible with generic computers. Allowing for both re-use and testing of the embedded application on a PC.

The goal is to use the same code on all these targets, only using conditional compilation on a feature basis.

### Concurrency model

As mentioned in the introduction, I want to use this queue to transfer data from interupt context to main context or vice versa. 

This implies the following:
* All operations must complete their action in a fixed, bounded number of instructions;
* Operations may not block, spin,or retry;
* Interrupts will always be enabled, otherwise data can be lost.
* The previous also means any operation itself can be interrupted.

This means the implementation has to be wait-free.

Given the wait-free requirements, it is also good to avoid operating system dependencies, as these can introduce undeterministic delays. And implementing the queue in standard C++ avoids external depencencies.

### Limitations

There will not be any DMA support.

### Testing requirements

Initial unit-testing will be done on a PC, together with several benchmarks to compare different implementations.

Once integrated into an embedded application, the queue will be tested as part of integration tests. There are currently no plans to perform unit-testing on target.

### Capacity: bounding or unbounded

The queue size can either be bounded (fixed) or unbounded (dynamic), this impacts run-time behaviour and the kind of memory used.

With a fixed capacity, the queue size is predetermined and stable during runtime, also no (re)-allocations. With a dynamic capacity, the queue can grow/shrink depending on run-time usage.

Regarding the kind of memory, fixed capacity queues can place their data either on the stack or on the heap. In case of a dynamic capacity, the data has be placed on the heap.

Since I am focussing on embedded systems, dynamic allocation during run-time is not an option. And if allowed, limited to an initialisation phase. This implies a fixed size queue. Whether the data is placed on the heap or stack is a choise, in this case I prefer the stack as this makes memory requirements explicit.

### Capacity: power of 2

> TODO

Allow for quick indexing, does limit tuning of queue size.
Optional configuration? -> impact on testing?
 * fast indexing with bit mask and therby avoiding modulo
 

### Blocking vs non-blocking

Getting data in and out of the queue will be done via the `pop`/`push` modifiers. Now these operations can either block until there is data/space available, or implement a over/underflow policy and return inmediatly. 

Since I want to use these operations in interrupt context, with low latency and in a wait-free manner, we need to go for the non-blocking implementation. This means `pop`/`push` return inmediatly and need to indicate wether their operation was successful or failed.

### Backpressure policy

Operations `pop` and `push` require a policy in case the queue is empty or full. For example, when the queue is full and new data is pushed, does `push`:

* spin and continously check if there is space to place the new element?
* yield and allow for another thread to possibly make space for the new data?
* sleep and retry;
* drop the latest/oldest element;
* overwrite the oldest element;
* some variation or combination of the above.

As I require non-blocking behaviour, waiting is not an option. This does mean selecting a policy which looses data when pushing new data. Given that data will be lost, I want `push` to drop the newest element and return an error signal. In case  blocking behaviour is required, a simple decorator will allow for this functionality later on.

Simalairly, `pop` will return inmediatly with a signal indicating if the returned data is valid.

To be able to detect if data has been lost, the queue will track this in the form of a counter. Similairly, there will be a counter when `pop` is called while the queue is empty.

### Element lifetime & memory management

The queue can be used to store the following data types:
* Primitive data types, such as bytes, integers, etc;
* Simple POD structures;
* Objects which can either be copied or moved.

The queue will manage the lifetime of any enqueued object for as long as the object is stored in the queue. Once popped, the consumer is responsible for the  lifetime and memeory management.

### Memory model & alignment

Given that Cortex-M is the main taget, data needs to be properly aligned to avoid unaligned exceptions. This means the internal data buffer must be properly aligned for the stored type.

Next to that, internal pointers/counters are requried to be atomic, thus limited to 32-bits.

For microcontrollers and PCs with data caches, we want to align the pointers/counters to the cache line size to avoid false sharing. In these cases, memory bariers will likely be needed.

### Summary

* Targetting ARM Cortex-M4/7/33 and generic PC;
* Used to transfer data from/to interrupt context;
* Low latency and wait free: non-blocking API;
* Fixed capacity: defined at compile-time;
* Backpressure policy: drop new data when full and a return error signal when empty;
* Element lifetime: managed by the queue while stored;
* Memory model & alignment: proper datatype alignment and optional cache alignment;
* Tracks error statistics: elements dropped, pop while empty;
* Portability: feature-based conditional compilation. 

> How to test each?
> batch modifiers?
> Worst-case execution time -> no loops, no dynamic memory, no disabling of irq

Properties
 * Retains total order

## Design

### Basic data structure

Options: ring-buffer, list, deque

Ring buffer, or circular buffer, has a fixed block of memory (fixed capacity) and 2 pointers which wrap around to provide a continous buffer.

A list can provide unbounded capacity, as each node refers to the next node. However this also means each node can be anywhere in memory.

> Deque
> Lock free linked ring (scot)

Data: primtive data / POD
Memory ordering: release for producer, aquire for consumer
Cache: seperate cache lines + copy of head/tail
Backpressure: reject latest when full

Todo: power of 2 capacity & indexing
 * simple mask (AND) vs modulo
 * basic instruction vs either FPU or soft-fpu
> TODO: add to benchmark

Elements
* array of type T -> good for trivial/POD
* aligned storage + placement new -> for non-trivial types

TODO:
* simple POD / trivially copy
  Can use basic array of T
* Objects which need to be created in-place, non-trivial, move only
  `AlignedStorage`

### Indexing

Head/tail counters
Mask, modulo

### Memory ordering

* atomics
* bariers (DMB vs atomic?)
* cache line



# Scratchpad

> TODO: concurrency model: bare-metal (no RTOS) producer and consumer in different context -> atomic + memory ordering



```bash
sudo cpupower frequency-set --governor performance
./build/benchmark-ninja-gcc/benchmark/queue_spsc/Release/benchmark_queue_spsc --benchmark_min_time=5s
```

```bash
--------------------------------------------------------------------------------------------------------
Benchmark                                              Time             CPU   Iterations UserCounters...
--------------------------------------------------------------------------------------------------------
BM_QueueSpsc<QueueV1<int, 100'000>>/100000000 7436520301 ns   7434176850 ns            1 items_per_second=13.4514M/s
BM_QueueSpsc<QueueV2<int, 100'000>>/100000000 2491948784 ns   2490989109 ns            3 items_per_second=40.1447M/s
BM_QueueSpsc<QueueV3<int, 100'000>>/100000000 1899773307 ns   1873090305 ns            3 items_per_second=53.3877M/s
BM_QueueSpsc<QueueV4<int, 100'000>>/100000000 2088300980 ns   2088033872 ns            3 items_per_second=47.8919M/s
BM_QueueSpsc<QueueV5<int, 100'000>>/100000000  338641363 ns    338195298 ns           21 items_per_second=295.687M/s
BM_QueueSpsc<QueueV6<int, 100'000>>/100000000  331586611 ns    331201190 ns           21 items_per_second=301.931M/s
BM_QueueSpsc<QueueV7<int, 131'072>>/100000000  281274476 ns    280923424 ns           30 items_per_second=355.969M/s
```


## Inspirations

* [Erik Rigtorp - SPSCQueue](https://github.com/rigtorp/SPSCQueue) for caching the read and write index.

Compare
* std::mutex
* [Michael & Scott](https://www.cs.rochester.edu/~scott/papers/1996_PODC_queues.pdf)

Design and implement queues as an embedded software components.

Constraints:
 - Targets: embedded / microcontrollers (32-bits), and PC (amd64/arm64).

Use-cases:
 - Exchange data between context (main/interrupts/threads).

> move

> +1 for empty





2. 

3. Indexing (power of 2 capacity)

Wrap-around versus "infinite" indexing. Elements stored in the queue will be stored in an array, and both a read and write "pointer" or index are needed to point to the oldest data or lastly written slot.

Now, the indices must be limited to the size of the queue, it does not make sense to access data outside of the queue. There are a few ways to do this:

- apply modulo to any index manipulation, this will ensure indices always point to a valid slot.
- but modulo can be expansive, instruction wise, so an alternative is a manual wrap around with a simple branch.
- an alternative is to apply a mask. This does limit the capacity to a power of two, but a mask is a simple AND instruction and therefore fast. Additionally, since a mask is applied, the index is never reset until it wraps around. Then the question becomes, when will it wrap around. When using 64bit integers, you will likely not run into any issues.

Now, I do not want to constrain my queues to a power of 2, nor do I want to use 64-bit integers on a 32-bit platform as these will not be atomic anymore. This leaves modulo and manual wrap around. Modulo can be expensive instruction wise, especially when the microcontroller does not have a floating point unit (FPU) available (either hardware wise or allocated to an other function).

> atomic first mentioned.


 * V1: base implementation
 * V2: added memory orderings to the atomic operations.
 * V3: aligned storage for the read and write indices to different cache lines to avoid false sharing.
 * V4: replaced modulo with a branch to wrap around the indices.
 * V5: cache read/write indices.
 * V6: added likely/unlikely hints.
 *
 * Variation   | (items/s)
 * ----------- | -----------
 *  QueueV1    |  12.8153M/s
 *  QueueV2    |  60.1057M/s
 *  QueueV3    |  78.4198M/s
 *  QueueV4    |  66.4483M/s
 *  QueueV5    | 152.294M/s
 *  QueueV6    | 177.823M/s
 *

[SPSC Lock-free, Wait-free Fifo from the Ground Up](https://www.youtube.com/watch?v=K3P_Lmq6pw0&t=611s) with [code](https://github.com/CharlesFrasch/cppcon2023/)
> todo: sanitizers

> wait-free
> lock-free
