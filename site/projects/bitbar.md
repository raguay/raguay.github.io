---
title: BitBar Scripts
date: 2018-11-15 18:32:06
---
## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}


[BitBar](https://getbitbar.com/) is a great program for putting custom icons in the macOS menubar. Check out my [tutorial on BitBar](https://computers.tutsplus.com/tutorials/customize-the-menu-bar-with-bitbar--cms-26946).

### Current Files Plugin


This plugin allows you to quickly edit commonly edited files using a selected editor. This  plugin works with the BitBar Alfred workflow, but is usable by itself. This plugin requires three files in your home directory:

- .myCurrentFiles

A list of all files that you want to appear in the menu. One file per line with it's complete path. You can use ~ for the home directory, but it has to be the first character in the line.

- .myeditors

This is a list of editors that you want to use with the plugin. It will be shown in the editor list. The format is {Name displayed}|{command or path to the executable}. The only editors that currently have a command setup is `sublime`, `emacs`, and `vim`. You will need to change the plugin for the executable paths of these editors.

- .myeditorchoice

This is the current editor being used by the plugin. It will contain either `sublime`, `emacs`, `vim`, or the path to the program.

I describe this plugin in detail in my [tutorial on Bitbar](https://computers.tutsplus.com/tutorials/customize-the-menu-bar-with-bitbar--cms-26946). The tutorial has a download for the Alfred BitBar workflow as well.

