---
title: Markdown to Presentation Workflow
date: 2018-11-12 14:44:18
---
## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}


This workflow assumes that the kramdown ruby package is installed on the system already. To install, simply type in a command line:
```bash
	gem install kramdown
```

Some system might require a sudo for this command. If you get an error message, try:

```bash
sudo gem install kramdown
```

This has a single file action that takes the given markdown file and converts it to a slide show in HTML and CSS.

The command **mds:theme** is used to set the theme. It will let the user pick from a list of themes.

The command **mds:showtheme** shows the user the currently set theme.

This workflow comes from my tutorial [How to Create a Slideshow Presentation From Markdown Notes](https://computers.tutsplus.com/tutorials/how-to-create-a-slideshow-presentation-from-markdown-notes--cms-23062).

More coming soon...

