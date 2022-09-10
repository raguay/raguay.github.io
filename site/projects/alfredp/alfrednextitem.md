---
title: Next Item Workflow
date: 2018-11-12 16:46:48
---
## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}


This little workflow allows you to sequentially step through items in multiple list files. You use the "Next Item: Set File" file action on the file containing a list of items: One item per line. For example, a list of urls; one per line. Then the hot key will take the next item from the specified first list and copy it to the clipboard and to a notification. If you view all lists before the first list, you will see each corresponding item for each list. The counter is only incremented after passing the item from the first list.

| Command | Description |
| --- | --- |
| ni:move # | This will move the last set file to the # list. If you do not move the file items to a list number, then it will not get sent to you. |
| ni:item | This will give the next item from the first list and increment the counter. |
| ni:l # | This will give the next item from the # list, but the count will not be incremented unless it is list 1. |
| ni:inc and ni:dec | These will increment or decrement the counter.  |
| ni:set | allows you to set the counter to any number.  |
| ni:clear | will clear the counter and erase the temporary files.  |
| ni:current | will display the current count number. |

The items are addressed using a zero reference. Therefore, if the counter is 1, the the second line in the file will be displayed.

Setting a new list will clear the count. The file specified is copied to a work area that all the other scripts will use to access it. Therefore, you do not need to worry about the original file being changed.


