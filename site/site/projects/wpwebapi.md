---
title: WordPress Web API
date: 2018-11-15 17:23:23
menu: "Projects"
---
## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}


## Web API

Many times when a site powered by WordPress wants to supply a Web API for their site, they will work outside of WordPress using either PHP or Ruby on Rails. Then they have to write their own functions to get to the information inside the database for their WordPress site. I always thought that was a little backwards. That is why I wrote the Web API plugin for WordPress.


With the Web API plugin, you no longer have to do that. This plugin creates a custom post type called API. When you create an API post, all of the content will be executed as PHP code just before the theme stuff is executed in WordPress. Therefore, you have full access to all the WordPress PHP functions to create whatever you want: JSON output, HTML sniplets, full HTML pages without any of the sites theme or code, or anything else you can imagine. After the code on the page is executed, then the PHP session will be ended.


## Features


- Create any type of Web API functionality
	- JSON output
	- Special HTML web sniplets to be included in another website or JavaScript powered widget.
	- Special web pages without any WordPress theming. Great for doing a special web application.
	- Anything else you can dream up!
- Place any PHP you want into the special API post type and it will be executed.

## Download

This is avaiable on my GitHub accout. [Check it out!](https://github.com/raguay/cct_api)

{{> 'donate.html'}}
