---
title: TextSoap Cleaners
date: 2018-11-15 17:38:04
menu: "Projects"
---
## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}


If you process a lot of text, you know the value of programs that will make that job easier. I used to use [Awk](http://en.wikipedia.org/wiki/AWK) for those text cleanup jobs, but now I have found a better friend: [Textsoap](http://www.unmarked.com/textsoap/)! Creating and sharing Textsoap cleaners is easy and fun.

As I write new cleaners, I will add them to the list below. You can use them as they are or modify them as you need. It is really easy. I also have an [Alfred workflow for working with TextSoap](/#/projects/alfredp/alfredtextsoap).

##### Cleaners

| Name | Description |
| ---- | ----------- |
| [Fix Bible Text.tscleaner](https://github.com/raguay/MyTextsoap/blob/master/Fix%20Bible%20Text.tscleaner)| This cleaner takes text copied from a theWord bible program and formats it the way I like it. |
| [Make Title from URL.tscleaner](https://github.com/raguay/MyTextsoap/blob/master/Make%20Title%20from%20URL.tscleaner) | This takes the slug out of an URL and creates a title from it. |
| [Name:Address converter.tscleaner](https://github.com/raguay/MyTextsoap/blob/master/Name:Address%20converter.tscleaner) | This one takes a list of &lt;name&gt;:&lt;address&gt; and creates an unordered list of anchors. |
| [PostURL to Title.tscleaner](https://github.com/raguay/MyTextsoap/blob/master/PostURL%20to%20Title.tscleaner) | Same as Make Title from URL.tscleaner except it assumes the slug is the text given. |
| [Remove Hyphens.tscleaner](https://github.com/raguay/MyTextsoap/blob/master/Remove%20Hyphens.tscleaner) | Remove all Hyphens and make them spaces. |
| [Remove dashes.tscleaner](https://github.com/raguay/MyTextsoap/blob/master/Remove%20dashes.tscleaner) | Remove all dashes and makes them spaces. |
| [Remove p tag.tscleaner](Remove p tag.tscleaner) | Remove all html p tags for including into WordPress. |
| [list of addresses to unordered list anchors.tscleaner](https://github.com/raguay/MyTextsoap/blob/master/list%20of%20addresses%20to%20unordered%20list%20anchors.tscleaner)| Takes a list of Urls and makes an unordered list of anchors for them. |
| [CleantoMinHTML](https://github.com/raguay/MyTextsoap/blob/master/CleantoMinHTML.tscleaner)|This cleaner will take HTML, remove all styling tags, remove all paragraph tags, but leave list type tags and anchor tags. This cleaner is great for taking expressive HTML to the bare minimum for inclusion into a CMS. |


##### Textsoap Article

I have also written an article on writing cleaners for Mac Tuts+. It is called:

- [How to Effortlessly Create Markdown With TextSoap](http://computers.tutsplus.com/tutorials/how-to-effortlessly-create-markdown-with-textsoap--mac-55744)
   This is a complicated cleaner that takes markdown text, translates it to HTML, and fixes it up to work in a WordPress page post.


