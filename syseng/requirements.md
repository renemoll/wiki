---
title: Requirements
description: 
published: true
date: 2023-07-16T13:51:23.130Z
tags: 
editor: markdown
dateCreated: 2022-12-20T15:14:28.578Z
---

# Requirements

* [EARS](https://alistairmavin.com/ears/)


# Requirements for requirements

(insert your xzibit image here)

Requirements focus on the **what**. What are the needs, constrains and such. The **how** is part of the concept design.

# Characteristics

Requirements should have a number of characteristics to
1. comply with the development process
1. be understandable for the people reading them

| Attribute | Description |
| --- | --- |
| Specific | Focus on a single aspect of what is needed. |
| Unambiguous | To ensure the readers share the same expection. |
| Complete | Are the assumption(s), scenario(s), environment(s), clear? |
| Correctness | Requirements and their assumptions must be correct. | 
| Tracable | (1) A requirements should be uniquely indentifyable for reference. (2) A requirements must orignate from somewhere. |
| Measureable | To verify the requirements |
| Quantifiable | Performance metrics and margins. |

## Examples

**Bad example**: The (product) must be user-friendly.

 - This requirements is not specific. It is not clear what is considered `user-friendly` in this context nor what could contribue towards achieving it. User friendlyness is actually a goal, which can be achieved by defining, mock-up and testing of a few user-scenarios and include acceptable ones as requirements.

# Checklist

Is each requirement:
* understandable? -> is it defined simple and consice.
* free of implementation? -> focus on **what** and not **how**.
* free of operations? -> ex: no requirements on a operator should use/make/maintain the product.
* a single statement? -> one specific element.
* is it needed? What would happen if this requirement was not included?
* are the assumption(s) correct?
* is it (technically) feasable?

Is the whole set of requirments
* compelete? Are aspects missing? Performance, interfacing, environment, manufactering, installation, training, safety, security?
* consistent? In terms of no contradicting requirements and use of language.

# References

1. Systems Architecting, A Business Perspective. Gerrit Muller.
1. NASA
1. INCOSE
1. SMART
