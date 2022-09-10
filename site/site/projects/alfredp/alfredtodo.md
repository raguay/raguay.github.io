---
title: Todo Workflow
date: 11-02-2018
---

## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}

This workflow is for working with todo lists using [TaskPaper](http://www.hogbaysoftware.com/products/taskpaper) or [FoldingText](http://www.foldingtext.com/). But, you can set any other editor you want as well. Since TaskPaper uses plain text files for everything, it is easy to write scripts to add functionality that the program does not have. So far, I have the following keywords defined:

| Command | Description |
| --------:| ---------- |
| t:settodo | This command allows you to set the directory for your todos. It will setup the supporting files and sub-directories as  well. This is the first action to perform with this workflow. |
| t:createtodaytodo | This command will take the everyday, weekly, monthly, and dated todos and combine them to the left over todos from the last time you created todos. It will also archive the finished todos. Todos that are repeated from the dated category are reset according to the repeat pattern.|
| t:showtoday | This command will open todays (or the most current) todo list in TaskPaper.  |
| t:showyesterday | This command will open yesterdays (or the one before the most current) todo list in TaskPaper.  |
| t:showfinished | This command will open the archived done tasks in TaskPaper.  |
| t:addmonthlytodo | This command will ask for the day of the month and the task. It will then place that in the monthly todo  directory for that day. When a new todo list is created, then it will pull in that days tasks. |
| t:addeveryday | This adds a task to the everyday task list. Every task placed in this list will be added to the current todo list everytime it is created.|
| t:addweekdaytask | This command will ask for the day of the week and the task. It will  then place that it in the weekly todo directory for that day of the week. When a new todo list is created, then it will pull in that days tasks. |
| t:doing | This creates a new dated entry for the current journal. It will ask which journal to place the entry into. The standard  doing.txt journal will automatically be created. |
| t:showdoing | This opens the current doing journal in TaskPaper.  |
| t:showprojects | This opens the projects task file in TaskPaper. This is for ongoing projects and their tasks.  |
| t:sortdone | This command takes the topmost TaskPaper list and sorts all of the done tag entries to the bottom.  |
| t:seteditor | This command is for setting the text editor to use.  |
| t:newjournal | This command will allow you to create new journal files.  |
| t:showjournal | This command is for opening a journal in the editor. It will ask which journal and give you the current list of  journals. |
| t:settz | This command is for setting the time zone. A list of time zones will be given and you select the one you are in.  |
| t:showtz | This command will show the currently set time zone.  |
| t:next | This finds the tag @next, marks that task done, and adds it to the next task. |
| t:adddatedtask | This allows you to add a task on a particular date that can repeat also. You can repeat by days, weeks, months, or years. It also shows all dated tasks and allows for deleting them. |
| t:managemonthly | This allows you to pick a monthly task and edit the file or delete the file. |
| t:manageweekly | This allows you to pick a weekly task to edit or delete. |
| t:editeverydaytask | This allows you to edit the everyday task file. |


