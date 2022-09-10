---
title: "Now Using a Svelte Powered Website on GitHub"
date: "2019-10-29"
---

## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}

This site is now running from [GitHub](https://GitHub.com) using 
[Svelte](https://svelte.dev). The main index page and the about page
is compiled as a built-in page, but all the other pages are dynamically
loaded from GitHub as a markdown page. The page has front matter is two
different formats that is processed and passed to a [Handlebars](https://handlebarsjs.com) processor.
It is then converted to HTML using the [Showdown](https://github.com/showdownjs/showdown) library.

It add new stuff, I just write the files in markdown in the directory for the
GitHub repository and perform a `git commit -am 'added new entry'; git push`. 
It is then live on GitHub. So far, it is working great!

I still have to fill out my side bar and add a few more bells and whistles, but
the bulk of the work is done and working smoothly. Down the road, I'm going to
write a tutorial about it.

It is so much fun to create your own CMS system!
