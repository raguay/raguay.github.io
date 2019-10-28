---
title: Haskel Text Converter Workflow
date: 2018-11-12 13:48:45
---
## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}


This workflow demonstrates the Haskell Alfred Library. The workflow allows text to be converted to different formats. The following commands are:

**ht:conv**

This command takes a string in the Alfred Prompt. You then pick the type of conversion you want. The result is pushed on to the clipboard.

**ht:start**

This command starts a dedicated web server for performing the text conversion.

**ht:stop**

This command closes the dedicated web server.

There is a **hotkey** for numbering the lines of text in the clipboard.

There is also an external trigger for taking text from the clipboard and allowing the user to select a converter. There is a **hotkey** for triggering that external trigger also that takes the current selection and puts it into the clipboard.


