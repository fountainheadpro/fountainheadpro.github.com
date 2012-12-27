---
layout: post
title: "Software Abstractions: What's wrong with your process"
description: "Limitaitons of existing software development methodologies for new project development"
category:
tags: []
---
{% include JB/setup %}

[DDD]: http://en.wikipedia.org/wiki/Domain-driven_design
[TDD]: http://en.wikipedia.org/wiki/Test-driven_development
[AP]: http://en.wikipedia.org/wiki/Agile_software_development


* This will become a table of contents (this text will be scraped).
{:toc}

There are well known processes and methodologies, which currently used by most of the teams:

* [Agile Process][AP],
* [Domain Driven Design][DDD]
* [Test Driven Development][TDD].

#Agile
While Agile brings a lot of great ideas, which are really useful it still built around the idea of existing stakeholder or customer. While iterative at it's core, it does not help in picking the  good abstractions. Instead, the development team is encouraged to continuously re-factor the code keeping it clean. The idea of self organization and emerging architecture prevails discussions on how to structure the code.

Based on my experience, the architecture does not always emerge in natural way.


[Domain Driven Design][DDD] meant to address this challenge by helping to define the domain model, which will wrup the code around the business model.

#Domain Driven Design
DDD is very helpful to organize the existing project or build the structure for well established business.
It set's the process for analyzing the business and structuring the software around the business model.
I has a lot of good ideas, but it does not provide good ideas on how to setup the model flexible enough to iterate quickly on the model itself.

#Test Driven Development
Test driven development is a backbone of iterative development process.
It goes hand in hand with agile helping to keep your code well tested and, really, it enables continuous re-factoring.
