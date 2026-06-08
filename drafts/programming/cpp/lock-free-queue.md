---
title: Lock free queue
description: 
published: true
date: 2026-06-08T14:35:05.236Z
tags: 
editor: markdown
dateCreated: 2025-08-28T19:25:03.156Z
---

# Lock free queue



Compare
* std::mutex
* [Michael & Scott](https://www.cs.rochester.edu/~scott/papers/1996_PODC_queues.pdf)

Design and implement queues as an embedded software components.

Constraints:
 - Targets: embedded / microcontrollers (32-bits), and PC (amd64/arm64).

Use-cases:
 - Exchange data between context (main/interrupts/threads).

> FIFO behaviour
> overwrite or not
> move

# Single producer single consumer queue

First, lets go through the design of a single producer, single consumer queue. The main use-case will be to transfer data from an interrupt to either the main loop or another interrupt. 

## Design considerations

### Capacity: fixed or dynamic

The first decision is if the queue size is fixed or dynamic. This impacts the kind of memory used. In case of a fixed capacity, the queue data can either be allocated on the stack of heap. For a dynamic capacity, the queue elements will live on the heap.

Since I am focussing on embedded systems, dynamic allocation during run-time is not done. And if allowed, limited to an initialisation phase. This implies a fixed size queue. Wether is lives on the heap or stack is a choise, in this case I prefer the stack as this makes memory requirements explicit.

### API: adding/comsuming data

For this queue I want standard FIFO behaviour, using `push` to add the latest element and `pop` to remove the oldest. 

### Blocking vs non-blocking

Tied to the modifiers, `pop`/`push` can either block till there is data/space or fail when they cant perform their operation. 

As I will be using this queue in interrupt contexts, I need non-blocking functions to make sure interrupt time can be bounded/limited. This means  `push` will fail when there is no empty space left and `pop` fails when the queue is empty.

In case I do need blocking behaviour, this can simply be added with a simple decorator.







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
