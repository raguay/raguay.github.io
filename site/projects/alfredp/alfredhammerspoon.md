---
title: Hammerspoon Workflow
date: 2018-11-12 14:52:10
---
## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}


This is a direct port of my Mjolnir Workflow.

This workflow is for running scripts using Hammerspoon to control your windows. This is just a sample of the things that can be done. Follow this layout and you can do many neat things with Hammerspoon.

First off, download Hammerspoon from https://github.com/Hammerspoon/hammerspoon/releases/latest.  Once installed, reload Hammerspoon and run the "hs:install" to set the configuration file this workflow expects. After that, everything should just work.

**hs:install**

Configure Hammerspoon with the configuration file that this workflow needs. The original is backed up into the users home directory as hs.orig.

**hs:reload**

This tells Hammerspoon to reload the configuration file.

**hs:open**

This opens the Hammerspoon console to the foreground.

**hs:nup**

This nudges the current window up.

**hs:ndown**

This nudges the current window down.

**hs:nleft**

This nudges the current window to the left.

**hs:nright**

This nudges the current window to the right.

**hs:tcaff**

This toggles system caffenate.

**hs:leftthirds**

This moves the current window to the left 1/3 of the screen.

**hs:rightthirds**

This moves the current window to the right 2/3 of the screen.

**hs:lefthalf**

This moves the current window to the left half of the screen.

**hs:righthalf**

This moves the current window to the right half of the screen.

**hs:tophalf**
This moves the current window to the top half of the screen.

**hs:bottomhalf**
This moves the current window to the bottom half of the screen.

**hs:fullScreen**
This moves the window to the maximum size on the screen.

**hs:minimize**
This minimizes the current window.

**hs:tzoom**
This toggles the system fullscreen on and off for the current window. This moves the window to it's own space taking up the entire screen.

**hs:running**
This will list all the running apps. You can then just select one to bring it to the front, select with alt key to hide it, select with ctrl key to unhide it, and select with the fn key to close the application.

**hs:snap**

This snaps the current window to the closes grid box area.

**hs:setgrid**

This requires you to put the x, y for a starting position in a 3x3 matrix for the current window. Then you give the width and height. Therefore, to move the current window to the upper left most block in a 3x3 matric, you would do "hs:setgrid 0, 0, 1, 1". There is also a hotkey set to this value as an example.

**hs:command**

Type in a command string and it will be sent to Hammerspoon directly!

There is also an external trigger HammerspoonCommand that will pass whatever is sent in the trigger to Hammerspoon using the command processor as in "hs:command". This gives other workflows or scripts the ability to interact with Hammerspoon through Alfred.

**hs:expose**

This will list all applications. When an application is selected, it will show all of it's windows in a matrix on the screen and ask the user for the coordinates of the one to show. It will then put all the windows back to their original position and bring the one selected to the foreground. If the application has only one window, it will simply bring it to the front.

I also created a hotkey for doing Expose on FoldingText. The user can create more in the same manner. Just be careful to get the name of the application correct!

**hs:last**

This command undoes the very last window move. This assumes all window movements were done with Hammerspoon and this workflow functions.


