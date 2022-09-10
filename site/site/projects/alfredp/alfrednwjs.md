---
title: NW.js Workflow
date: 2018-11-12 15:07:47
---
## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}


NW.js is an application for developing applications using web technologies. You can create an application with HTML, CSS, and JavaScript using any io.js (formerly node.js) library. There has been a move to this new version due to the node.js project in a stalemate and far behind in development compared to what Chrome is using.


Once you have your application developed, you can zip it up with a config.json file.


The workflow provides the following commands:

| Command | Description |
| ---- | --- |
| nw:website | This opens the NW.js website on GitHub. If you hold down the &lt;cmd&gt; key, it will open the io.js website. |
| nw:open | When the user starts typing, a file ending in the ".nw" extension is looked for according to the work typed. Therefore, if there is a file called "new.nw", as soon as "n" is typed , that file will be displayed. |
| nw:opendir | Opens the current directory in Finder or Path Finder using Node Webkit. The config.json file should be in that directory. |
| nw:help | Opens this help program. |


There are also two File Actions defined: *Open Directory* that is available on directories, and *Open NW.js Package* that is available on NW.js packages.


There are also two External Triggers: *RunNWjsDirectory* and *RunNWjsPackage* which work the same as the file actions. These allow external programs or other Alfred workflows to call a Node Webkit application by passing the full path of the application bundle or directory. The help option for this workflow shows an example of using these External Triggers.


The following code will open the help application that is located in the same directory as the code:

```php
thisDir=`pwd`;

/usr/bin/osascript -e "tell application \"Alfred 2\" to run trigger \"RunNWjsDirectory\" in workflow \"com.customct.NWjs\" with argument \"$thisDir/help\""
```

The directory path given in the argument tells NW.js where to load the program. It is set with the *pwd* command.


There will be more tutorials and hacks using this workflow on my website [Custom Computer Tools](http://customct.com).

