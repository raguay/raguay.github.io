---
title: eLisp Extensions
date: 2018-12-31 08:14:45
menu: "Projects"
---
## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}


I'm back to using Emacs and eLisp again. I haven't done much with it since my college days in the `80s. Here are some items I've been working on:

## [Teacode Expand](https://github.com/raguay/TeaCode-Expand)

This elisp package defines the command `teacode-expand` which can be assigned to a hotkey using this:

```elisp
(global-set-key (kbd "C-A-e") 'teacode-expand)
```

Once assigned, pressing the hotkey will take the current line, pass it and the extension of the file associated to the buffer, and send it to the [TeaCode](https://www.apptorium.com/teacode). TeaCode will find an expansion for it and return the results which is then pasted back in place.

The GitHub page tells how to add it to your Emacs config. Enjoy!
