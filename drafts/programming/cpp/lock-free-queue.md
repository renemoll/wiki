---
title: Lock free queue
description: 
published: true
date: 2026-06-17T11:36:00.507Z
tags: 
editor: markdown
dateCreated: 2025-08-28T19:25:03.156Z
---

# Single producer single consumer queue

> TODO: non-blocking, wait free


First, lets go through the design of a single producer, single consumer queue. The main use-case will be to transfer data from an interrupt to either the main loop or another interrupt. 

## Design considerations

### Target machine

I target 32-bit microcontrollers, gennerally single core but with several interrupts.

### Capacity: bounding or unbounded

The first decision is if the queue size is fixed (bounded) or dynamic (unbounded), as this impacts run-time behaviour and the kind of memory used.

With a fixed capacity, the queue size is predetermined and stable during runtime, also no (re)-allocations. With a dynamic capacity, the queue can grow/shrink depending on the needs at run-time at the cost of variable latency at possible blocking system calls.

Regarding the memory, fixed capacity queues can either place their on the stack or on the heap. In case of a dynamic capacity, the data has be placed on the heap.

Since I am focussing on embedded systems, dynamic allocation during run-time is not done. And if allowed, limited to an initialisation phase. This implies a fixed size queue. Whether the data is placed on the heap or stack is a choise, in this case I prefer the stack as this makes memory requirements explicit.

### Queue policy

For this queue I want simple FIFO behaviour, using `push` to add the latest element and `pop` to remove the oldest.

### Blocking vs non-blocking

The modifiers, `pop`/`push`, can either block till there is data/space available or implement a over/underflow policy and return inmediatly. 

As I will be using this queue in interrupt contexts, I need non-blocking functions to ensure interrupt time can be bounded.

### Backpressure policy

Modifiers such as `pop` and `push` require a policy in case the queue is empty or full. For example, when the queue is full and new data is pushed, does `push`:

* spin and continously check if there is space to place the new element?
* yield and allow for another thread to possibly make space for the new data?
* sleep and retry;
* drop the latest/oldest element;
* overwrite the oldest element;
* some variation or combination of the above.

Given I require non-blocking behaviour, waiting is not an option. This does mean selecting a policy which looses data. Given that data will be lost, I want `push` to drop the newest element and return an error signal. In case  blocking behaviour is required, a simple decorator will allow for this functionality later on.

Simalairly, `pop` will return an error signal when there is no data to return.

### Element lifetime / memory management

TODO:
* simple POD / trivially copy
  Can use basic array of T
* Objects which need to be created in-place, non-trivial, move only
  `AlignedStorage`



### Requirements

* Fixed capacity, defined at compile-time;
* FIFO behaviour, using `push` and `pop` modifiers;
* Low latency, which implies: non-blocking API and no system/OS calls;

* Backpressure policy: drop new data and a return error signal;
* Track statistics, such as elements dropped;

> How to test each?
> batch modifiers?

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

# Scratchpad

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
