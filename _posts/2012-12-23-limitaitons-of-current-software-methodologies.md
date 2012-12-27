---
layout: post
title: "Limitaitons of current software methodologies"
description: ""
category: 
tags: []
---
{% include JB/setup %}

<div class='toc'>
	<ol>
		<li>Agile</li>
		<li>Domain Driven Design Much longer shit</li>
		<li>TDD</li>
	</ol>
</div>

[DDD]: http://en.wikipedia.org/wiki/Domain-driven_design	
[TDD]: http://en.wikipedia.org/wiki/Test-driven_development
[AP]: http://en.wikipedia.org/wiki/Agile_software_development


There are well known processes and methodologies, which currently used by most of the teams:
* [Agile Process][AP], 
* [Domain Driven Design][DDD]
* [Test Driven Development][TDD]. 

## Limitations of Agile
While Agile brings a lot of great ideas, which are really useful it still built around the idea of existing steakholder or customer. While iterative at it's core, it does not define good process for picking the right good abstractions.
Instead, the development team is encouraged to continuesly refactor the code. 

[Domain Driven Design][DDD] meant to address this challenge by helping to define the domain model, which will wrup the code around the business model.

## Limitations Domain Driven Design
DDD is very helpful to organize the existing project or build the structure for well established business.
It set's the process for analysing the business and structuring the software around the business model.
I has a lot of good ideas, but it does not provide good ideas on how to setup the model flexible enough to iterate quickly on the model itself.

## Limitations of Test Driven Development 
Test driven development is a backbone of iterative development process. 
It goes hand in hand with agile helping to keep 
