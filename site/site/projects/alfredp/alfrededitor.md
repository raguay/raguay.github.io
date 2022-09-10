---
title: Alfred Editor
date: 2018-11-12 15:05:40
draft: false
---
## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}


This is a simple editor that makes use of **Node Webkit Toolbox** to run. Therefore, you need to install that workflow first. After installing this workflow, you need to execute **ae:install** to install the data files and the help files into their proper location. You will have a command line program called **ae** you can use to open files from the command line.

The following commands are then useable:

**ae:openeditor**

This simply opens Alfred Editor without a file.

**ae:edit**

The currently selected file in Path Finder or Finder is opened in Alfred Editor. You also have an Alfred Browser command for opening files as well. An external command for opening files is available as well.

**ae:open**

This script filter gives several important directory locations that can be opened in the Alfred browser or Finder.

**ae:theme**

This script filter lists all the available themes. If you select one, that will be the new theme for windows opened in Alfred Editor. If you hold the **command key** while selecting, that theme will be opened in Alfred Editor to edit.

**ae:createtheme**

This allows you to create a new theme to use in Alfred Editor. It will request a new name, create the new theme from lesser-dark them, and open in Alfred Editor to edit. You will still have to select the theme for it to be used.

**ae:windowlist**

This will list each available Alfred Editor window name. The one selected will be brought to the front using the Mjolnir Workflow. The Mjolnir workflow has to be installed for this command to work.

**ae:keyboard**

This command allows you to choose either the Sublime keyboard layout or the Vim keyboard layout to use in Alfred Editor. If the Sublime layout is chosen, then the status line will always show it to be in insert mode.

This workflow is a work in progress. I am currently working on a command prompt similar to Sublime with expandability using plugins. I also currently have only three themes. If you want to help me create themes, just send me the json file for your theme and I will include it.

