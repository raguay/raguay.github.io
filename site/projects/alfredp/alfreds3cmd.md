---
title: s3cmd Workflow
date: 2018-11-12 17:45:03
---
## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}


This workflow gives the ability to upload files to Amazon S3 using the s3cmd commandline function. You can download the s3cmd utility at [http://s3tools.org/s3cmd](http://s3tools.org/s3cmd). The workflow currently contains a copy of the s3cmd tool. You will need to open a terminal to the directory that contains the workflow to set your s3 credentials. Please see the directions at [http://s3tools.org/s3cmd](http://s3tools.org/s3cmd) to know how to set it up. Here are the currently supported keywords and file actions:

| Command | Description |
| --- | --- |
| s3c:copydir | This keywork allows you to pick a directory that contains videos (mp4|mov). The videos will be copied to the corresponding directory on s3. Make sure to set the base directory using "s3c:base". |
| s3c:base | You use this keyword to set the base directory for s3. It should be the format of "s3://{bucket}/directory/..". It has to be set to "s3://{bucket name}" as the minimum. |
| s3c:target | This keyword is used to set a target directory under the base directory to copy individual files to s3 using the file action. |
| s3c:webheader | This keyword is used to set a web header for getting a web friendly url to an item in your s3. |
| s3c:sbase | This will show the base directory in a notification. |
| s3c:starget | This will show the target directory in a notification. |
| s3c:swebheader | This will show the header to make a web friendly address in a notification. |
| s3c:copy file | This file action will copy the file in the Alfred browser to the base and target directory on s3. |
| s3c:list | This keyword action allows you to browse your S3 directory. If you hit "cmd-enter" on an item, it will download it to your Download directory. If you hit "alt-enter" on an item, it will set that directory as your target directory for uploading files. If you hit "ctl-enter" on an item, it will push a web facing friendly url for that item in to the clipboard. If you hit "shift-enter" on an item, it will set the items directory as the base directory for future browsing. If you hit "function-enter" on an item, you can move the item to a new name or location. It will prompt for the new location with a copy of the original item twice. You change the second one. If you start typing after the keyword, your selection will be reduced to selections that match what you type. |
| s3c:configure | This keyword will open a terminal and start the configuration process for the s3cmd command line tool. This has to be done before using the other commands. |

