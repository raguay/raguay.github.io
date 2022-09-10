---
title: Alfred URI Handler
date: 2018-11-12 15:35:19
---
## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}


This workflow has one command "au:install". Once you run it, a URI handler for Alfred will be installed. This is used to trigger external triggers in any workflow. The format is:

alfreduri://com.apple.AppleScript.AlfredURIhandler?wf=&lt;workflow Bundle ID&gt;&amp;arg=&lt;arguments&gt;&amp;ext=&lt;external trigger name&gt;

The arguments should be URI encoded (ie: no spaces, but %20 instead). If you update the workflow, you have to re-apply the handler. Also, do not delete the workflow or the functionality will be removed.

You can also launch a search in Alfred with:

alfreduri://com.apple.AppleScript.AlfredURIhandler?search=&lt;search query&gt;

The search query needs to be URI encoded as well.


