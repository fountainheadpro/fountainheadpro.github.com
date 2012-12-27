---
layout: post
title: "Iterating to find the right software abstractions"
description: "Iterating on abstractions"
category:
tags: [architecture, iteration, modeling]
---
{% include JB/setup %}

This post will describe the process for iterative development, which will also help zero down to the right abstractions while iterating on the functionality. I found it really applicable in startup environment, when no established business processes can give the answers to what functionality will be implemented.

* This will become a table of contents (this text will be scraped).
{:toc}

Talking to many project steak-holders, I found that many people think about implementing system functionality in the same way as publishing content. It seems logical, that web site features should be brought live, tested, altered as needed and then possibly removed if proved unneeded.
It does not seem to anyone that the new functionality can make the overall system more complex and contribute to increase the amount of work the team will need to develop further features.

In this situation, it's hard to overestimate the importance of the right software abstractions.
Here is what MIT Professor Daniel Jackson has to say about it:

>Pick the right ones, and programming will flow naturally from design; modules will have small and simple interfaces; and new functionality will more likely fit in without extensive reorganization. Pick the wrong ones, and programming will be a series of nasty surprises: interfaces will become baroque and clumsy as they are forced to accommodate unanticipated interactions, and even the simplest of changes will be hard to make. <a  target="_blank" href='http://www.quora.com/Software-Engineering/What-makes-a-good-engineering-culture/answer/Edmond-Lau'>Quora: What makes a good engineering culture?</a>


# Write it in your language
When I think about the new functionality, which will be iterated upon, I start from taking and simple use-case and build a json file, which will   describe my use case.

Let's take a simple example:
You are building a product catalog for eCommerce web site. The web site is pretty simple.
It's just a simple product page describing the product, it should have product image, price and add to car button.
The home page will have links to your product pages.
No need to extra complexity.

Well, except, that  down the road you will need to go on to add promotions, relevant products, it will have special prices for special gold club visitors, it will have product reviews, product ratings. If it's a book you will need to look inside the book feature. Who knows what else will come? Let's not over-architect  it right now and build only what users need right now.

Now let's implement it in json:






# Implement your DSL


# Iterate