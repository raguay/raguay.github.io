---
title: Thai Translation Workflow
date: 2018-11-12 12:55:41
---
## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}


This workflow does web scraping on the http://www.thai-language.com/ site to translate words from english to thai/thai to english. It does an exact match first. If the exact match fails, then it does an inexact match. Consequently, the results do not always produce what you would expect all the time.

Remember to set the result count with “tt:setcount”!

**tt:engthai**
Translate an English word to Thai.

**tt:thaieng**
Translate a Thai word to English.

**tt:setcount**
Set the number of results to display to the user.



