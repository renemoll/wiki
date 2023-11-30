---
title: driver-abstractions
description: 
published: true
date: 2023-11-30T1:11:42.458Z
tags: 
editor: markdown
dateCreated: 2023-11-30T1:11:42.458Z
---


# Step 1: basics

```c++
class timer0 {
public:
	enum clock_select: uint8_t {
		clock_off,
		io_clk,
		io_clk_1_8th,
		io_clk_1_64th,
		io_clk_1_256th,
		io_clk_1_1024th,
		ext_clk_rising,
		ext_clk_falling
	}

	timer0(clock_select cs, uint8_t max);

	// no copy as this is placed on the register map
	timer0	(timer0 const&) = delete;
	timer0& operator=(timer0 const&) = delete;

	uint8_t get_count() const;

private:
	enum interrupt_source: uint8_t {
		overflow = 1,
		ocra_match = 1 << 1,
		ocrb_match = 1 << 2,
	}

	static constexpr uint8_t count_mode_a {0x03};
	static constexpr uint8_t count_mode_b {0x08};

	// actual device registers, hence no additional members allowed!
	uint8_t volatile TCCRA;
	uint8_t volatile TCCRB;
	uint8_t volatile TCNT;
	uint8_t volatile OCRA;
	uint8_t volatile OCRB;
}


uint8_t volatile &TIMSK0 {*reinterpret_cast<uint8_t*>(0x6E)};


timer0::timer0(clock_select cs, uint8_t max):
	TCCRA{count_mode_a},
	TCCRB{count_mode_b | cs},
	OCRA{max}
{
	TIMSK0 |= overflow;
}

uint8_t timer0::get_count() const
{
	return TCNT;
}

```


Instanciate on memory map:
```c++
void* const t0_addr {reinterpret_cast<void*>(0x44)};
timer0& t0 {*new (t0_addr) timer0{timer0::io_clk_1_64th, 250}};
```

And add interrupt handler

# Step 2: trait example

Now, what if we have multiple timers with different functionality?

```c++


struct timer0_traits {
	static uint8_t volatile &TIMSK {*reinterpret_cast<uint8_t*>(0x6E)};

	enum clock_select: uint8_t {
		clock_off,
		io_clk,
		io_clk_1_8th,
		io_clk_1_64th,
		io_clk_1_256th,
		io_clk_1_1024th,
		ext_clk_rising,
		ext_clk_falling
	}
};

struct timer2_traits {
	static uint8_t volatile &TIMSK {*reinterpret_cast<uint8_t*>(0x70)};

	enum clock_select: uint8_t {
		clock_off,
		io_clk,
		io_clk_1_8th,
		io_clk_1_32th,
		io_clk_1_64th,
		io_clk_1_128th,
		io_clk_1_256th,
		io_clk_1_1024th,
	}
};

template <typename timer_traits>
class timer8_t {
public:
	using clock_select = typename timer_traits::clock_select;

	timer8_t(clock_select cs, uint8_t max);

	// no copy as this is placed on the register map
	timer8_t (timer8_t const&) = delete;
	timer8_t& operator=(timer8_t const&) = delete;

	uint8_t get_count() const;

private:
	enum interrupt_source: uint8_t {
		overflow = 1,
		ocra_match = 1 << 1,
		ocrb_match = 1 << 2,
	}

	static constexpr uint8_t count_mode_a {0x03};
	static constexpr uint8_t count_mode_b {0x08};

	// actual device registers, hence no additional members allowed!
	uint8_t volatile TCCRA;
	uint8_t volatile TCCRB;
	uint8_t volatile TCNT;
	uint8_t volatile OCRA;
	uint8_t volatile OCRB;
};

template <typename timer_traits>
timer8_t<typename timer_traits>::timer8_t(clock_select cs, uint8_t max):
	TCCRA{count_mode_a},
	TCCRB{count_mode_b | cs},
	OCRA{max}
{
	timer_traits::TIMSK |= overflow;
}

template <typename timer_traits>
uint8_t timer8_t<typename timer_traits>::get_count() const
{
	return TCNT;
}

using timer0 = timer8_t<timer0_traits>;
using timer2 = timer8_t<timer2_traits>;

void* const t2_addr {reinterpret_cast<void*>(0xB0)};
timer2& t2 {*new (t2_addr) timer2{timer2::io_clk_1_64th, 250}};
```


## Improvements: avoid address mismatch

1. add addres to trait
```
struct timer0_traits {
	static constexpt std::uintptr_t addr{0x44};
	static uint8_t volatile &TIMSK {*reinterpret_cast<uint8_t*>(0x6E)};

	enum clock_select: uint8_t {
		clock_off,
		io_clk,
		io_clk_1_8th,
		io_clk_1_64th,
		io_clk_1_256th,
		io_clk_1_1024th,
		ext_clk_rising,
		ext_clk_falling
	}
};
```
1. overload new
```
template <typename timer_traits>
class timer_8_t {
public:
	static void* operator new(std::size_t) {
		return reinterprest_cast<void*>(timer_traits::addr);
	}

	static void* operator delete(void *) {
	}
}

timer0& t0 {*new timer0 {timer0::io_clk_1_64th, 250}};
timer2& t2 {*new timer2 {timer2::io_clk_1_64th, 250}};
```

# Part 3: add different timers (8 + 16 bits)

```
enum standard_clock_select: uint8_t {
	clock_off,
	io_clk,
	io_clk_1_8th,
	io_clk_1_64th,
	io_clk_1_256th,
	io_clk_1_1024th,
	ext_clk_rising,
	ext_clk_falling
}

struct timer0_traits {
	static constexpt std::uintptr_t addr{0x44};
	static uint8_t volatile &TIMSK {*reinterpret_cast<uint8_t*>(0x6E)};

	using clock_select = standard_clock_select;
	using count_t = uint8_t;
}

struct timer1_traits {
	static constexpt std::uintptr_t addr{0x80};
	static uint8_t volatile &TIMSK {*reinterpret_cast<uint8_t*>(0x6F)};

	using clock_select = standard_clock_select;
	using count_t = uint16_t;
};

struct timer2_traits {
	static constexpt std::uintptr_t addr{0xB0};
	static uint8_t volatile &TIMSK {*reinterpret_cast<uint8_t*>(0x70)};

	// only used by this type
	enum clock_select: uint8_t {
		clock_off,
		io_clk,
		io_clk_1_8th,
		io_clk_1_32th,
		io_clk_1_64th,
		io_clk_1_128th,
		io_clk_1_256th,
		io_clk_1_1024th,
	}

	using count_t = uint8_t;
}


template <typename timer_traits>
class timer8_t {
public:
	using clock_select = typename timer_traits::clock_select;
	using count_t = typename timer_traits::count_t;

	timer8_t(clock_select cs, count_t max);

	// no copy as this is placed on the register map
	timer8_t (timer8_t const&) = delete;
	timer8_t& operator=(timer8_t const&) = delete;

	count_t get_count() const;

private:
	enum interrupt_source: uint8_t {
		overflow = 1,
		ocra_match = 1 << 1,
		ocrb_match = 1 << 2,
	}

	static constexpr uint8_t count_mode_a {0x03};
	static constexpr uint8_t count_mode_b {0x08};

	// actual device registers, hence no additional members allowed!
	uint8_t volatile TCCRA;
	uint8_t volatile TCCRB;
	uint8_t volatile TCNT;
	uint8_t volatile OCRA;
	uint8_t volatile OCRB;
};
```

# Notes

* Still needs an interface on `timer8_t` to be able to be independent of specific types.
* RMO: Could pass the traits back to the interface via CRTP?


Check out:
> Andrei Alexandrescu wrote about this in Modern C++ Design calling it Policy-based design
> Strategy pattern?
> embedded-hal
