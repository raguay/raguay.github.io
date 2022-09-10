---
title: Sermon Scheduler Workflow
date: 2018-11-12 18:48:47
---
## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}


This workflow aid in the creating of my sermon schedules. Use ss:setdirectory to set the directory for sermons (or whatever you want to create schedules from a template). The use ss:seteditor to set the editor you want to use (I use Sublime). You then can use ss:create to make a new schedule by the template (you might want to edit the template first with the ss:edit and selecting the template). Then use ss:edit to edit one of the schedules or the template.

The unique thing about the workflow is that new schedule’s name will always be something like: 2014-Feb02-Feb08.md. The current year, first day of the week and the last day of the week. The ss:create gives you names for the current week and the next 4 weeks.

This works great for me being a missionary. You can change it to meet your own needs.

