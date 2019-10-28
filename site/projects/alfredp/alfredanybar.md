---
title: Anybar Workflow
date: 2018-11-12 14:39:35
---
## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}

This workflow requires the anybar application to be install. The easiest way to install is by home-brew cask:

brew cask install anybar

If you do not have HomeBrew installed, follow the instructions here: [HomeBrew](http://brew.sh/). Then execute the above line.

Once installed, you can use the features of this workflow:

**anybar:launch**
Launches anybar with optional port number.

**anybar:setgraphic**
Set the graphic for the anybar application. It will give a list of usable graphics. Start typing and the list will be narrowed down to the ones that match. Select the one and the last launched Anybar will be changed to that graphic.

**anybar:setport**
This allows you to set the port number of the AnyBar app.

**anybar:setup**
This copies the graphics I created to the ~/.AnyBar directory.

There is a file action, Copy to Anybar,  that will copy a png graphic to the ~/.AnyBar directory so that it can be used with the program.

There are two External Triggers: SetGraphic and Launch. The SetGraphic external trigger expects a string with the name of the graphic, a '|', and a port number. The Launch external trigger expects a UDP port number to launch the AnyBar program on.

