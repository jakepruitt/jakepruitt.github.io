---
layout: post
title: Chameleon
image: /images/chameleon.jpg
description: Imitation is the greatest form of flattery, and also the easiest way to start coding.
---

![](/images/chameleon.jpg)

I have long been convinced that I am not good at learning languages. During a Spanish test in the middle of junior year, I had to sit with my teacher and describe the story shown in a few pictures of a cat climbing a tree. Rather than saying "The cat climbed the tree", I accidentally said, "The cat set the tree on fire". Surprisingly enough, those two phrases are just one syllable apart in Spanish.

I was terrible at speaking Spanish, but I was pretty good at conjugating verbs. There was a pattern, and plenty of tables, and I could fill those out with no problem. I read the book, and memorized grammar very well, but I could not speak Spanish to save my life.

The reason I could not speak Spanish was that I had never listened to how Spanish speakers talk, and never had a model to copy off of. I had heard tape recordings of Spanish speakers, but never interacted with people enough to start mimicking the way they spoke, and repeating the phrases until I felt comfortable with everyday words. If I wanted to really learn fluency in Spanish, I should have moved to Spain or Mexico and spent all of my time talking with Spanish speakers.

The same goes for becoming fluent in code.

## the first HTML page

After watching online videos and reading books and tutorials and articles about HTML and CSS, I was tasked with working on a project with the development team at work. I looked at the picture of the page I had to build, and looked back at the blank screen and had no idea where to even begin. I knew there needed to be a `<head>` and a `<body>` section, but after that I had no clue about how to make tabs, or how to set up a style sheet, or what class names to give anything. I did not know if I needed margins or absolute positioning or floats or even flex-boxes. I knew what each of those things meant, and I could answer quiz questions about those properties, but I could not figure out how to apply them.

This was very similar to knowing the grammar of Spanish but never learning how to say it. I knew the rules, I just did not know the common idioms or phrasing that made the applied language so rich and expressive. I needed a voice to copy, and thankfully I had a mentor at the time named Dennis.

## the D.E.N.N.I.S system

Dennis had a system to the way he built a front-end. This system does not have an acronym to the letters of his name, but if you want one of those, you should watch "It's Always Sunny in Philadelphia".

Dennis always constructed the raw HTML first, with no styles, to make sure it worked from a structural standpoint. He made sure things were semantic, meaning that every element on the page had a purpose and was being used for that purpose consistently. He made sure images appeared in a logical order with their headings or descriptions.

He then took to the stylesheets, marked off sections with comments, and began doing his craft of painting a page. He preferred inline styles, styles that look like this:

```CSS
.header { width:90px; margin:0 10px 0 10px; }
.header .breadcrumb { color:#3124ee; }
```

I was incredibly thankful to finally have a style that I could emulate. I did not know whether this was a good style or not, but after seeing the way he wrote styles, I quickly emulated him and worked like a clone of Dennis, creating styles the way he did and building pages with markup first.

I needed that first push in the right direction to really get my first thoughts across. Without anything to copy, it's like using a razor for first time. You don't even know how it's supposed to work, even if you know how blades theoretically move around and hairs are typically cut. You need some sort of role model, and Dennis was my role model from the very first day.

Nowadays I still keep a lot of the styles that I inherited from Dennis, but have defined a style of my own. I think we do the same in speaking languages and in writing.

My recommendation, if you are thinking of writing your first HTML page is to find a website that you like that doesn't have too much JavaScript functionality, copy all of the HTML code when you "View Source" into your own HTML file. Then click around in the developer tools until you find the main styleguide, which you can usually find by inspecting element and clicking on the line number next to any style. Copy all of those styles into a CSS file by the same name in the right directory pattern on your computer. Then, if you feel comfortable playing around, try adding another tab to the menu, or changing all of the images upside-down, or giving the site an entirely different color scheme.

Learning by chameleon is how we learned most things growing up, and it's how I learned the biggest lessons in web development.