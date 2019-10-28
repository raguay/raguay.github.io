---
title: Title Case Server Workflow
date: 2018-11-12 19:04:42
---
## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}


This workflow goes with an upcoming tutorial on using golang with Alfred on tutplus.com. It currently runs a small web app for doing title case conversions. The workflow has these commands:

| Command | Description |
| --- | --- |
| tcs:launch | This will start the title case server on port 9910 |
| tcs:stop | This will stop the title case server |
| tcs:convert | This will take a string on the Alfred prompt, send it to the title case server, and return the result in a notification and the clipboard. |

It also has a hotkey specified to take the selected text, convert it, and paste it back in place. You will have to set the hotkey yourself. The go source code is included in the workflow.

