---
title: Textsoap Cleaners Workflow
date: 2018-11-12 17:38:47
---
## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}


This workflow interfaces with [TextSoap](http://www.unmarked.com/textsoap/), a great text processing program. I now use it more than awk! The following are the keywords defined:

| Command | Description |
|---|---|
| tc:clean | This keyword will present a list of all previously used cleaners to pick from. Start typing to narrow down the list. When you hit enter on an entry, it will perform that cleaner on the clipboard. If you hold down the fn key, it will delete that cleaner from the list of preferred cleaners. You can set a hotkey to repeat the last ran cleaner on the clipboard. |
| tc:full | This keyword will show all available cleaners obtained from the tc:getcleaners. The cleaner you select will be performed on the clipboard and the cleaner will be saved into your list of preferred cleaners. |
| tc:fulla | This keyword is the same as tc:full, but will append the results to the topmost application.  You can set a hotkey to perform this on the current selection as well.|
| tc:seteditor | Allows you to set the text editor for editing the list of preferred cleaners. |
| tc:editlist | Allows you to edit the list of preferred cleaners using the editor already setup. |
| tc:getcleaners | This will query TextSoap for the list of cleaners it has. You should do this each time you create new cleaners you want to use with this workflow. |
| tc:addcleaner | This will set the string given into the list of preferred cleaners. |
| tc:count | This will count the number of lines, words, and characters in the clipboard. If a string is passed with it, it will count that string. You can set a hotkey to count the current selection. |
|tc:loadpopclipext  | This will load the popclip extension for executing the last cleaner on the highlighted text.|

There are also three places to set your hotkeys: one for doing a character/word/line count of your selection, one for evoking the last cleaner on selected text, and one for choosing from the full list of cleaner to apply on the currently selected text.


