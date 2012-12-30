---
layout: post
title: "JSONit methodology: Iterating to find the right software abstractions"
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
Let's take a simple example:

You are building a product catalog for eCommerce web site. The web site is pretty simple.
It's just a simple product page describing the product, it should have product image, price and add to car button.
We have three product types:
  - Books. Can come in paperback or hardcover.
  - T-shirts, which are come in multiple sizes and colors.
  - Cups - come in different colors and sizes.

Down the road we might need to go on to add promotions, relevant products, it will have special prices for special gold club visitors, it will have product reviews, product ratings. There will be more product categories. Let's not over-architect  it right now and build only what the team needs right now.

Here are couple of problems, which arise around using common frameworks like Java/spring, ruby/Rails, javascript/backbone:
1. How do we structure the model? Should product class have t-shirt size property as well as the book author?
Should we have a base product class and a subclass for each product category?  Will we have to create new subclass every time we introduce the new product category?
2. How to structure the presentation layer? We know how to map the model to the page using template mechanisms. Do we have separate page for each category? Do we have one page and build some kind of widget mechanism which will allow dynamically adding necessary features depending on the product type?
Question here, do these established frameworks provide good language to describe our product page to enable fast iterations and avoid clatter.

When I think about the new functionality, which will be iterated upon, I start from taking and simple use-case and build a json file, which will describe my use case. Reason I pick json is it's so easy to read and operate with this format in any language. 

Let's experiment in json to find the best language for our situation:

Here is sample *book* product description:
{% highlight json %}
{
 "category": "book",
 "title": "Robinson Crusoe",
 "author" : "Daniel Defoe",
 "description" : "Robinson Crusoe is a novel by Daniel Defoe that was first published in 1719...",
 "formats" : [
   {
     "type":"Paperback",
     "price":"4.95"
   },
  {
     "type":"Hardcover",
     "price":"7.95"
   }   
   ]
}
{% endhighlight %}
Here is sample *t-shirt* product description:
{% highlight json %}
{
 "category": "t-shirt",
 "colors": ["blue","orange","red","white"],
 "description" : "This t-shit will make you feel like giant bunny rabbit is hugging you.",
 "sizes" : [
   {
    "size-range": ["XXS", "XS", "S", "M", "L"],
    "price" : "17.95"
   },
   {
    "size-range": ["XL", "XXL"],
    "price" : "19.95"
   },
   ]
}
{% endhighlight %}

Just based on quick look at this data it is clear that certain data fields will need to be presented as widgets on the page. Like color, size selector or book formats.

Let's think how these widgets can be structured.
Again, we can start from defining our widgets in json:

ColorPicker widget:
{% highlight json %}
{
  "name" : "color-picker",
  "field" : "colors",
  "position" : "left", 
  "style" : "drop-down"  
}
{% endhighlight %}
SizePicker widget:
{% highlight json %}
{
  "name" : "size-picker",
  "field" : "sizes",
  "position" : "bottom", 
  "style" : "horizontal-list",  
}
{% endhighlight %}

As you can see each widget knows which field it represents.
This structure also opens possibilities for experimenting with different options to present size and color choices (drop-down vs. horizontal-list) as well as experimenting with positioning of elements.

# Implement your DSL
coming soon




# Iterate

coming soon
