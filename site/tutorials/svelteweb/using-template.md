---
date: 2019-12-06
title: Using the Svelte GitHub Website Template
---

# {{title}}

#### {{cdate date 'MMMM D, YYYY'}}

Many want to run a simple blog or a small website without spending a whole lot of
money. They often believe they have to sacrifice speed and flexibility to get it
going cheap enough for them. But, the truth is, you can create a website for free!

This tutorial will show you how you can create your own website with simple
markdown files and a [GitHub Pages](https://pages.github.com/) account. You are
going to build a site using the [Svelte framework](https://svelte.dev/) and the
[Svelte GitHub Website Template](https://github.com/raguay/SvelteGithubSiteTemplate).

This template creates everything you need to get a working website going on your
computer, and then putting it on the web using [GitHub](https://GitHub.com). Since it
is basically a flat file system website, you will not need to install a full web server
stack. The Svelte installation supplies a Node.js based development server with live
reload to view your site as you are building it.

This template has partials for taking pieces of code and placing it in your site where ever
you need it in the markdown pages. It also has a macro expansion ability based on
[Handlebars](https://handlebarsjs.com/) with some added helpers that I've designed. Since your
pages are created using [markdown](https://daringfireball.net/projects/markdown/basics),
it would be good to become familiar with how it works.

## Tools you will need

You will need to have [Node.js](https://nodejs.org/en/), [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git),
[Mask](https://github.com/jakedeichert/mask) task runner, a web browser, and a text editor. You don't have to have
Mask, but I do highly recommend using it. I'm personally
using the [Oni 2](https://v2.onivim.io/) editor for writing and programming, but you can use any editor
that you are used to using.

I'm working on a macOS system, but any computer system that can run the above tools should work fine. If you are on
windows, you might need to use the [Maid](https://github.com/egoist/maid) task runner instead. Mask is a
Rust program and hasn't been tested on Windows much, but Maid is a Node.js program and should run anywhere
that Node.js runs. I also show all the steps for making your own scripts if you don't want to use
a script runner.

## Downloading the Template and Running the Development Server

In a terminal program, like [Kitty](https://github.com/kovidgoyal/kitty), go to the directory you would like your
website directory. In that directory, run the following command line:

<hr />
```bash

npx degit raguay/SvelteGithubSiteTemplate <project name>
cd <project name>

```
<hr />

The `<project name>` is the name you give your website. Therefore, if you want the directory for your website to be
called `MyBlog`, then use `MyBlog` instead of `<project name>`. The above command lines become:

<hr />
```bash
npx degit raguay/SvelteGithubSiteTemplate MyBlog
cd MyBlog
```
<hr />

Now you are in the website directory. The website directory should have a directory/file
structure as shown (tree is a unix command for showing the current directory down in a
graphical tree structure):

```bash
 $ tree
├── LICENSE
├── README.md
├── launch
│  ├── README.md
│  ├── css
│  │  └── bundle.css
│  ├── index.html
│  └── js
│      └── bundle.js
├── maskfile.md
├── package.json
├── public
│  ├── CNAME
│  ├── bundle.css
│  ├── bundle.css.map
│  ├── bundle.js
│  ├── bundle.js.map
│  ├── index.html
│  └── site
│      ├── 404.md
│      ├── blog
│      │  ├── index.md
│      │  └── my-first-post.md
│      └── parts
│          └── test.html
├── rollup.config.js
└── src
    ├── WebSite.svelte
    ├── components
    │  ├── About.svexy
    │  ├── BlogPosts.svelte
    │  ├── Footer.svelte
    │  ├── Index.svexy
    │  ├── Logo.svelte
    │  ├── NavBar.svelte
    │  ├── Page.svelte
    │  ├── Sidebar.svelte
    │  └── Twitter.svelte
    ├── main.js
    └── store
        └── infoStore.js

10 directories, 31 files
```

Next, run the npm command to install the node.js libraries needed to work on this website:

<hr />
```bash
npm install
```
<hr />

This takes a while if you've never installed some of the node.js packages. On my system, it
took 44 seconds. Once done, you can now run the development server and see what your website
looks like:

<hr />
```bash
npm run dev
```
<hr />

When you see the `waiting for changes...` in the terminal, your site has been compiles and is
running on a local server. You can open a browser and view your site at `http://localhost:5000`.
The local server puts code into your site to auto refresh your browser whenever you change any
file in the `src` directory. When you do, it will recompile the code and force a refresh on your
browser.

## The Two Types of Pages

There are two types of pages in this template: a Svelte component and markdown files. In the
current site, the `About.svexy` and `Index.svexy` components are for the main site index page
(ie: the front page of your website), and the about page. These can be any valid Svelte component.
In this template, they are markdown files that use [Mdsvex](https://github.com/pngwn/MDsveX). Mdsvex
is a markdown type file that is compiled into a normal Svelte component and added to the `bundle.js`
file. Therefore, these pages are always loaded into the browser of the person looking at your site.
You should keep these types of pages as minimal as possible to keep your load time as fast as
possible.

To see the minimal code for one of these pages, look at the `About.svexy` file in the `src/components`
directory:

<hr />
&#96;&#96;&#96;js exec
```
  import { fade } from 'svelte/transition';
  import { onMount } from 'svelte';
  import { info } from '../store/infoStore.js';

  let styles = {};

  onMount(() => {
    //
    // Subscribe to the information store to get the site information.
    //
    const unsubscribeInfo = info.subscribe((value) => {
      styles = value.styles;
    });

    return () => { unsubscribeInfo(); };
  });
```
&#96;&#96;&#96;

&#96;&#96;&#96;css style
```
  .box {
    width: 100%;
    margin: auto;
    padding: 10px;
    margin-top: 10px;
    margin-bottom: 10px;
  }
```
&#96;&#96;&#96;

&lt;div class="box" style='border: &#123;styles.borderSize&#125; solid &#123;styles.borderColor&#125;; border-radius: &#123;styles.borderRadius&#125;; background-color: &#123;styles.divColor&#125;; background-image: &#123;styles.divBackgroundPicture&#125;; color: &#123;styles.textColor&#125;;" in:fade="&#123;duration: 500&#125;"'&gt;

```markdown
## About Us

This is a markdown file with information about you. Change as
you see fit.

The `div` setup the proper styling for the markdown and controls
the animation of it on the site. Thereore, leave the div information
as it is and just change the markdown inbetween.
```

&lt;/div&gt;
<hr />

There are two code blocks that the Mdsevx package will include in the module as JavaScript and CSS. The **&grave;&grave;&grave;js exec**
code block is added as JavaScript to the created Svelte code and the **&grave;&grave;&grave;css style** is added to the Svelte CSS block.
The style block sets the styling for the `div` element to show it properly on the site. The JavaScript section loads
the Svelte code needed to get the styling information from the `info` store and the fade directive for the `div`
block. Just add the markdown you want in the area between the `<div>` and `</div>` elements.

If you want to include other components, just load them in the JavaScript section just like any other
Svelte component and put the markup in the place you want it to be in the markdown. Just like standard
markdown, you can mix in HTML code as needed. This makes for a very versatile  page creation. Anything
you want to do can be done in these pages!

The other type of page is the markdown pages. They are any page under the `site` directory in the `public` and `launch` folders. Any page
request that doesn't match a Svelte component in the router is expected to have a corresponding markdown file. For example, the page
`localhost:5000/blog/index` will send the file `public/site/blog/index.md` to the user to see.

If a file request is sent that doesn't match a component or a markdown file in the system, then the `public/site/404.md` file will
be processed and sent to the viewer. This file is actually preloaded when the partials are preloaded. You will
see how to load partials in the next section.

These markdown files are limited to plain markdown, any registered Handlebars helpers, and everything that is in the YAML header
is avaliable as a Handelbar helper. Here are a list of helpers I've added to the template:

| Helper | Description |
| --- | --------- |
| &#123;&#123;save &lt;name&gt; &lt;text&gt;&#125;&#125; | This command creates a helper named &lt;name&gt; with the expanding text of &lt;text&gt;. It also places the given &lt;text&gt; at the point of definition. This allows you to create text snippets on the fly inside the template. Very handy. |
| &#123;&#123;date &lt;format&gt;&#125;&#125; | This will format the current date and time as per the format string given. |
| &#123;&#123;cdate &lt;date/time&gt; &lt;format&gt;&#125;&#125; | This takes the date/time string and formats it according to the format given. |
| &#123;&#123;last &lt;weeks&gt; &lt;dow&gt; &lt;fmat&gt; | This will go back in time to &lt;weeks&gt; ago and give the date for the particular &lt;dow&gt; (Day Of Week) in the &lt;fmat&gt; format. |
| &#123;&#123;next &lt;weeks&gt; &lt;dow&gt; &lt;fmat&gt; | This will go forward in time to &lt;weeks&gt; ahead and give the date for the particular &lt;dow&gt; (Day Of Week) in the &lt;fmat&gt; format. |
| &#123;&#123;cDateMDY&#125;&#125; |  gives the current date in Month Day, 4-digit year format |
| &#123;&#123;cDateDMY&#125;&#125; |  gives the current date in Day Month 4-digit Year format |
| &#123;&#123;cDateDOWDMY&#125;&#125; |  gives the current date in Day of Week, Day Month 4-digit year format |
| &#123;&#123;cDateDOWMDY&#125;&#125; |  gives the current date in Day of Week Month Day, 4-digit year format |
| &#123;&#123;cDay&#125;&#125; |  gives the current date in Day format |
| &#123;&#123;cMonth&#125;&#125; |  gives the current date in Month format |
| &#123;&#123;cYear&#125;&#125; |  gives the current date in 4-digit year format |
| &#123;&#123;cMonthShort&#125;&#125; |  gives the current date in Short Month name format |
| &#123;&#123;cYearShort&#125;&#125; |  gives the current date in 2-digit year format |
| &#123;&#123;cDOW&#125;&#125; |  gives the current date in Day of Week format |
| &#123;&#123;cMDthYShort&#125;&#125; |  gives the current date in Month day 2-digit year format |
| &#123;&#123;cMDthY&#125;&#125; |  gives the current date in Month Day 4-digit year format |
| &#123;&#123;cHMSampm&#125;&#125; |  gives the current date in h:mm:ss a format |
| &#123;&#123;cHMampm&#125;&#125; |  gives the current date in h:mm a format |
| &#123;&#123;cHMS24&#125;&#125; |  gives the current date in H:mm:ss 24 hour format |
| &#123;&#123;cHM24&#125;&#125; |  gives the current date in H:mm 24 hour format |

The time formatting is done using the [Moment.js](https://momentjs.com/) library. Please refer to that website for the
details on how to create the format string.

These are the same helpers available in my Alfred Workflow [Quiver](/#/projects/alfredp/alfredquiver) and [Template](/#/projects/alfredp/alfredtemplate).
Those workflows are using the same base code I'm using with the Svelte GitHub Website Template project. Yes, I reuse stuff that I like! Please refer
to the [Handlebars](https://handlebarsjs.com/) documentation for any built in helpers.

If you want to add your own helpers, then add them to the `src/components/Pages.svelte` file. All helpers that are not time sensitive should
be placed in the `onMount()` function with the ones I have there. The helpers that are time sensitive should be placed in the `processData()`
function. For example, the **&#123;&#123;save &lt;name&gt; &lt;text&gt;&#125;&#125;** helper is in the `onMount()` function since it is saving
data on the page for use further in the page and isn't a time based function.

## Changing Site Information

All basic site information is kept in a Svelte store. Any component can access this information. The following is the baics found in the store:

<hr />
```javascript
import { writable } from 'svelte/store';

export const info = writable({
  siteName: 'Svelte Based Website on GitHub',
  byLine: 'Great framework for making websites.',
  address: 'http://localhost:5000',
  GitHub: '',
  parts: ['test.html'],
  local: true,
  styles: {
    backgroundColor: '#D1BD79',
    backgroundPicture: '',
    borderColor: '#AA7942',
    divColor: '#ECDAAC',
    divBackgroundPicture: '',
    borderSize: '5px',
    borderRadius: '10px',
    textColor: 'black',
    font: '20px Times New Romand, Arial',
    headerFont: '20px Verdana, Arial',
    showSideBar: true,
    sideBarLeft: false
  }
});
```
<hr />

The first thing you will need to change is the `siteName` and `byLine` fields. These will have the name for your website and it's by-line. If you
don't want a by-line, just leave it blank.

The `address` is the HTTP address for your local server. You will only need to change this
if you change the port for your local server.

The `GitHub` address is the full path to your `site` folder when you upload to your GitHub pages repository. Once it is uploaded,
go to the repository in GitHub, click on the `site` directory, then click on the `404.md` file, and select the `raw` button on the right.
You should now have the raw address to the `404.md` file and see the contents in the browser. Copying the address should give you:

<hr />
```sh
https://raw.githubusercontent.com/raguay/raguay.github.io/master/site/404.md
```
<hr />

Put everything up to the `site` in the variable `GitHub`. It should look similar to:

<hr />
```sh
    GitHub: 'https://raw.githubusercontent.com/raguay/raguay.github.io/master/site',
```
<hr />

Of course, it will have the name of your account instead of my `raguay` account. This will be where the
`Page.svelte` component will look for markdown pages for your site.

The `parts` variable is an array of names of files in the `site/parts` directory. Each file named
here will be loaded into Handlebars as a partial. You can then include it on any markdown
page using **&#123;&#123;> 'test.html'&#125;&#125;** macro. Each partial that is used
causes some delay on loading the first markdown page. You might want to keep the ones you
load to a minimum.

The `local` variable controls which address to use to get the pages: `address` or `GitHub`. If set to
true, the the `address` address is used. Otherwise, the `GitHub` address is used. Make sure this is
set to `false` and compiled before uploading to your GitHub site!

The `styles` object contains all the styling information for the site. Most of them are very self
explanitory as they are named similar to the CSS properties. If the `showSideBar` variable is set to
true, the side bar will be visible on the left side if `sideBarLeft` is true. It'll be on the right
if `sideBarLeft` is false. If `showSideBar` is false, then no side bars will be shown and the content
area will take the full with under the header.

These variables can be set programmically as well. That way, you can setup pages with the side bar or
without. You could also set all the styling information from a menu entry to have different styles
for each user. I'll most likely be adding more features for this in future versions of the template.

Each component that need information from the `info` store will have the following in it's script
block:

<hr />
```javascript
  import { onMount } from 'svelte';
  import { info } from '../store/infoStore.js';

  let styles = {};

  onMount(() => {
    //
    // Subscribe to the information store to get the site information.
    //
    const unsubscribeInfo = info.subscribe((value) => {
      styles = value.styles;
    });

    return () => { unsubscribeInfo(); };
  });

```
<hr />

The `onMount` function is imported from `svelte` and used to register a function that will run
whenever the component is mounted to the DOM. The `info` store is loaded from the file
that defines it. In the function ran by the `onMount` life cycle function will then
register a function to run each time the library `info` is updated. That function set
a component variable (I call it a shadow variable since it shadows the original store) to
the new value of the store. When updated, it will trigger a
refresh on the component. Now, you can use the information in the library in the
template and in other functions. Just be careful that a function doesn't get called before the
store's shadow variable isn't initialized.

When you subscribe to a store, the return value is the function to use to unsubscribe from the store. When
you return from a `onMount()` function call, you return a function that calls the unsubscribe
function to help free up memory and processing time for updates to the store. That function
is called whenever the component is unmounted (or removed from the DOM).

If you need to make sure you have the latest information from a store before going forward with a function,
you have to use the `get` function to get it from the store. The store variable that you load in isn't the
actual store, but accessor function to it. You get the `get` funtion this way:

<hr />
```javascript
  import { get } from 'svelte/store';
```
<hr />

You then use that function to get the most current value of the store. For example:

<hr />
```javascript
  var localvalue = get(info);
```
<hr />

Now, you can use `localvalue` just like you did `info` in the template. This is a read only variable. You can't set values in the
store by using the locally saved variable. To change a store's vaule, you use the `set()` method of the store. This only works if
the new value is different (ie: 1 instead of 0). But for structures, this might not always be the case. Be careful.

## Changing the Menus

The main menu on the website is in the `NavBar.svelte` component. It looks like this:

<hr />
```html
<div id='navbar' style="background-color: {styles.divColor};
                        background-image: {styles.divbackgroundPicture};
                        border: {styles.borderSize} solid {styles.borderColor};
                        border-radius: {styles.borderRadius};
                        color: {styles.textColor};" >
  <a class='navItem' href='/' use:link use:active>Home</a>
  <a class='navItem' href='/blog/index' use:link use:active>Blog</a>
  <a class='navItem' href='/about' use:link use:active>About</a>
</div>

<style>
  .navItem a {
    color: black;
    text-decoration-color: black;
  }

  #navbar {
    display: flex;
    flex-direction: row;
    width: 85%;
    margin: auto;
    border-radius: 10px;
    padding: 10px;
    margin-top: 10px;
    margin-bottom: 10px;
  }

  #navbar a {
    text-decoration: none;
    font-size: 24px;
  }

  .navItem {
    margin-right: 26px;
    text-decoration: none;
  }
</style>

<script>
  import { link } from 'svelte-spa-router';
  import active from 'svelte-spa-router/active';
  import { onMount } from 'svelte';
  import { info } from '../store/infoStore.js';

  let styles = {};

  onMount(() => {
    //
    // Subscribe to the information store to get the site information.
    //
    const unsubscribeInfo = info.subscribe((value) => {
      styles = value.styles;
    });

    return () => { unsubscribeInfo(); };
  });

</script>

```
<hr />

The items of interest in the `script` block is the importing of the `link` and `active`
commands. These are used in the template to define the anchor tags. The `use:link` action
in the anchors will fix the references to the local SPA router style. A normal anchor
reference would be `/blog/index`, the `link` action changes it to `/#/blog/index`. You
don't have to use the link action, but it does make it a little easier to read.

The `active` action will show the link that is currently being displayed with the
`active` class. You have to define your `active` class globally so that the name
doesn't get specialize for the component. It is currently defined in the `WebSite.svelte`
component in order to be only defined once. It looks like:

<hr />
```css
  :global(a.active) {
    color: #155393 !important;
    text-decoration-color: #155393;
  }

```
<hr />

The `:global()` command tells Svelte that this is a globally defined CSS value
and it should not be name mangled.

So, if you want to add a page call `Favorites` with the markdown file name of `favorites.md`, you
would add the following to the list of anchor tags in the template:

<hr />
```html
  <a class='navItem' href='/favorites' use:link use:active>Favorites</a>
```
<hr />

And make sure the file is in the `site` directory.

## Changing the Main, Sidebar, and Footer Components

The main page (or more often refered to as the index page) is in the file `Index.svexy` file. It
has the same layout as the `About.svexy` that we have already examined. Just add the markdown
text you want in the main page. You can also include other components if needed.

The Sidebar is in the `src/component/Sidebar.svelte` component and the Footer is in the `src/component/Footer.svelte` component.
They are nornal Svelte components that can be edited and changed as you need. Components like these that need to be edited are the
reason I've made this a template and not a library. There is a `src/components/Twitter.svelte` and `src/components/BlogPosts.svelte`
components that can be placed in the Sidebar as you want. I'll be creating more such components down the road.

## Adding General and Blog Pages

The format of the `site` directory is as follow:

```sh
public/site
├── 404.md
├── blog
│   ├── index.md
│   └── my-first-post.md
└── parts
    └── test.html
```

Everything under the `site` directory is available to be sent as a page. The items in the `parts` directory can be seen
as a page if they are markdown (ie: if the name of the file ends in `.md`). But, most partials will be html since
they are not processed through the markdown and Handlebars processors. But, I think I will be doing that in the future.

Every page needs to be a markdown file with the ending `.md`. The files in a subdirectory are accessed as the path is normally
seen. For example, the index for the blog page is `/blog/index`. For this reason, all directories should be a single word without
and spaces or anything that isn't a letter or a number (ie: all punctuation and special symbols).

There isn't currently a process for building the index page for a blog. You will have to do that yourself. I'm working at
adding a function to the Mask task runner for building the index pages from the post pages.

Every markdown page has to start with YAML head matter at the top. The minimum information is:

<hr />
&#45;&#45;&#45;<br>
&nbsp;&nbsp;title: The title of the blog<br>
&nbsp;&nbsp;date: 2019-11-26<br>
&#45;&#45;&#45;
<hr />

The format is basically a name, `:`, and a value. The name has to be a single word. The date is given in the `YYYY-MM-DD` format.
Each post can display it in any format given in the heading section as seen here:

<hr />
&#35; &#123;&#123;title&#125;&#125;<br>
&#35;&#35;&#35;&#35; &#123;&#123;cdate date 'MMMM D, YYYY'&#125;&#125;<br>
<hr />

The date is taken from the YAML head matter and formated using the `cdate` helper function. The format is the
[Moment.js](https://momentjs.com/) formating. You can change these to anything you want. This
is just the formatting that I'm using on my site.

Each variable in the YAML head matter is also accessable using the Handlebar helpers just as the `title` was
used in the above example.

The rest of the file is whatever markdown and text you want in your post or page.

## Build and Deploying the Site

I'm assuming that you already have a [GitHub Pages repository setup](https://guides.github.com/features/pages/). If not,
go ahead and do that. Once setup, clone the repository to the directory `launch`. That is best done by doing the
`git clone` command in the templates directory, copy the files/directories in the `launch` directory to that cloned
directory, delete the current `launch` directory, and rename the cloned git directory to `launch`. The build script will
place all your site's information into the lauch directory and upload it to GitHub.

Once the `launch` directory is setup, you can run:

<hr />
```sh
mask build 'initial launching'
```
<hr />

This will fully build the site, commit the changes to the git repository with the message given in single quotes, and
push the changes to the GitHub repository for your GitHub pages site. Once GitHub Pages syncs, your new site
will be live for everyone to see.

If you don't want to use Mask, then create a script with the following lines:

<hr />
```sh
#!/bin/sh
npm run build
rm -Rf launch/js launch/css launch/imgs launch/site
mkdir launch/css launch/js
cp public/*.js launch/js
cp public/*.css launch/css
cp -Rf public/imgs launch/
cp -Rf public/site launch
cp public/CNAME launch
cd launch
git commit -am "$1"
git push
```
<hr />

Then make the script executable using `chmod a+x` on the file. You should then be able to use that script instead
of the Mask script.

The file `CNAME` is the name of your site if your using your own domain name server
for the site. GitHub Pages will then use the name in that file as the name of the
webserver for your site.

## Conclusion

Now that you know how to use this website template, go and make your own websites using it.
Please let me know what sites you create with it so I can add it to the list on the
template's GitHub page. That way, everyone can see who is using this template.

