---
title: Text Massagers Workflow
date: 2018-11-12 16:54:11
---
## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}


I am often changing text around to different formats in large quantities. So, I made a workflow for keeping all of them. I call it text massagers because you are "massaging" the text with the script. You can use this as your template for your own massagers. All of these scripts takes the item from the clipboard, massages it, and places back into the clipboard while showing you the results.

|  Command | Description |
| --- | --- |
| <alt><command>m  | Expects a markdown anchor line in the clipboard and converts it to a HTML anchor within a list item.|
| <alt><command>t  | Fixes a time into HH:MM:SS format no matter what it was before. |
| <shift><command>” | Takes the current selection and passes it to the “tm:select” command for selecting the text massager from a list. The list will show the resulting string. It will then perform the selected “massage” to the text and copy it to the clipboard and back into the document it was grabbed from if possible. |
| tm:select | Takes the string on the Alfred Prompt and runs it through the different massagers and shows the output in the list. When the user selects one of the massagers, it will copy the resulting string to the clipboard and to the document that is open. |
| <shift><alt>" | Takes the current selection and passes it to the “tm:selectn” command for selecting the text massager from a list. It will then perform the selected “massage” to the text and copy it to the clipboard and back into the document it was grabbed from if possible. |
| tm:selectn | Same as "tm:select" except for not displaying the results in the list. This is for slower computers. | 
