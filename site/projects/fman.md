---
title: fman Extensions
date: 2018-11-15 18:10:50
menu: "Projects"
---
## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}


[fman](http://fman.io) is a flexible, extensible file manager for macOS, Linux, and Windows. You can extend fman's functionality by writing exensions in Python 3. I wrote a tutorial on writing extensions for fman on [TutsPlus](https://computers.tutsplus.com/tutorials/fman-the-extendable-file-manager-for-any-system--cms-28340).

I have been creating many entensions for fman. Each extension below has a link to the GitHub repository for the extension. To install an extension, in fman press the command prompt key (`<shift>+<cmd>+p`), type `install plugin`, and press the `<enter>` key. Fman will then show a list of plugins that you haven't installed yet. Select the extension you want and it will be usable after restarting fman.

If you have an ideal for an extension that you would like to see, send me a tweet at @CustomComputerT and I might just make it for you! I love creating extensions for the programs I use.

Here are the ones I've created so far:

- [Favorites](https://GitHub.com/raguay/favorites)

    The favorites extension gives you a way to store directories by a user defined name and go to that directory from a search list. It also allows you to create shortcut directories that allow you to specify directories relative to the shortcut. Then you can sync the file to another system, set the shortcut directory for that system, and use the same favorites!

    This extension also has four quick set and go to directory memories that are lost on rerunning fman. Just one hotkey to set and to go to that directory.

- [ProjectManager](https://GitHub.com/raguay/ProjectManager)

    The project manager extension allows you to set a directory as a project. When you enter a project directory for the first time (ie. Not already working in that project, but when working on a different project), it will run a script to set up you development environment.

    This extension will also show a list of project directories and allow you to go directly to them.

- [Swap Panels](https://GitHub.com/raguay/SwapPanels)

    The Swap Panel extension give you a hotkey to swap the directory shown in each panel. Simple little extension, but I use it a lot!

- [DeSelect](https://github.com/raguay/DeSelect)

    The DeSelect extension will deselect all selected file in the current file pane. Fman now has a built in for this.

- [DuplicateFileDir](https://github.com/raguay/DuplicateFileDir)

    This extension will make a duplicate of the file or directory under the cursor or selected. It will add the text '-copy' to the file or directory.

- [MoveToDir](https://github.com/raguay/MoveToDir)

    This extension allows you to move the selected file to a specific directory. If the directory doesn't exist, it creates it.

- [OpeniTerm2](https://github.com/raguay/OpeniTerm2)

    This extension is for macOS. It opens the current directory in iTerm 2 terminal emulator.

- [OpenWithEditor](https://github.com/raguay/OpenWithEditor)

    This macOS extension allows you to edit the current file in the editor that is selected in the [BitBar](https://getbitbar.com/) extension [currentFiles.1h.rb](https://getbitbar.com/plugins/System/currentFiles.1h.rb). You have to have the BitBar program and extension installed to use this extension.

- [SelectByRegExp](https://github.com/raguay/SelectByRegExp)

    This extension allows you to select files in the current file pane using a regular expression. It toggles the selection, so you can also use it to de-select files based on a regular expression.

- [ShowVideoFileProperties](https://github.com/raguay/ShowVideoFileProperties)

    This extension shows video file properties. It uses ffmpeg and that program has to be installed on your system.

- [VersionInfo](https://github.com/raguay/VersionInfo)

    This extension shows the current fman version, api version, and python version used in fman.

- [VimNavigation](https://github.com/raguay/VimNavigation)

    This extension allows you to navigate using Vim style keyboard shortcuts. You have to preceed them with a shift.

- [ZipSelected](https://github.com/raguay/ZipSelected)

    This extension zips all the selected files using the current directory as the name for the zip.

