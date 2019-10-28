---
title: Notes Workflow
date: 2018-11-12 17:56:11
---
## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}


This workflow if for taking notes. It was designed for Calca, but can be used with any editor. So far, I have the following keywords:

| Command | Description |
| --- | --- |
| n:setnotes | This allows for the setting for the location of your notes directory. It is a directory select. Therefore, the directory has to already exist. |
| n:notes | This will list every file in the notes directory that ends in ".txt". You can create a new notes file or open an existing notes file. If you select one of the files while holding the <cmd> key, you can append the contents of the clipboard to the specified notes file. If that is a new file, it will be started with the clipboard contents. You can move the selected file to the trash by holding the <fn> key. This requires the trash command to be in the "/usr/local/bin" directory. You can convert the markdown file to html using the <shift> key when you press <enter> on a file name. This requires the pandoc program to be loaded onto your system. The <alt> key will open the file with Marked.app. |
| n:setEditor | This allows you to set the editor that you want to use for editing your notes. It defaults to Calca, but you can set it to any application you want. It will bring up a file selector with applications from your main application folder and your personal applications folder. |

