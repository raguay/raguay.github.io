---
title: Template Workflow
date: 2018-11-12 13:38:49
---
## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}


This workflow allows you to create templates with Handlebar syntax. To use the workflow, you have to have Node.js installed first. I recommend using [Homebrew](http://brew.io) to install it.

Once Node.js is installed, go to your snippets directory in Alfred Browser and select the **Set Template Directory** file action. This tells the workflow where your templates (or snippets) are to be kept.

You then run the **tp:install** to install the example templates and a default global.json file. This file should be edited to match your needs. Any data item added to this file is then passed to the Handlebar render as data. All templates have to have the “.txt” extension. If you want data to be associated with a template, then place a JSON file with the same name as the template in the t

When you run **tp:expand** or **tp:exptext**, it will list all of your template files in the template directory. When you select one, it will be expanded with any json file with the same name and the global json file data. The **tp:expand** will put the result into your clipboard and the topmost application. The **tp:exptext** will give it to TextExpander to expand and place in the topmost application. With the **tp:exptext** command, TextExpander will also expand any of it’s macros in the template file. I mostly use it for placing the cursor after expansion. These two commands also have an associated Alfred Browser File action.

The **tp:open** command opens the template/snippet directory in Alfred Browser. If you press the Command key, it will open it in the Finder.

The **tp:editglobal** will open the global.json file in your template directory with the default editor for JSON files.

The **tp:create** command requires a name. A file with that name and a “txt” extension is created in the template directory and opened in the default editor for files with a “txt” extension.

The **tp:createclip** command is the same as the **tp:create**, but this command takes the current clipboard contents as the text for the file. It is then opened in the default editor for “txt” files.

The **tp:edittemplate** command will give a list of templates. When you choose one, it is opened in the default editor for a file with the “txt” extension.

The **tp:edittemplatedata** command will give a list of templates. When you choose one, it’s corresponding JSON file is opened in the default editor for a JSON file.

There are two special helper function for Handlebars defined. The helper functions given here are just the names. They have to be inside of two curly brackets to work. This is because I use the same system on my web server to expand macros. They are:

**save &lt;name&gt; &lt;text&gt;**
This command creates a helper named “&lt;name&gt;" with the expanding text of “&lt;text&gt;”. It also places the given “&lt;text&gt;” at the point of definition. This allows you to create text snippets on the fly inside the template. Very handy.

**clipboard**
This helper command places the current clipboard contents at the point in the template.


The following data expansions are defined as well:

**cDateMDY** gives the current date in Month Day, 4-digit year format

**cDateDMY** gives the current date in Day Month 4-digit Year format

**cDateDOWDMY** gives the current date in Day of Week, Day Month 4-digit year format

**cDateDOWMDY** gives the current date in Day of Week Month Day, 4-digit year format

**cDay** gives the current date in Day format

**cMonth** gives the current date in Month format

**cYear** gives the current date in 4-digit year format

**cMonthShort** gives the current date in Short Month name format

**cYearShort** gives the current date in 2-digit year format

**cDOW** gives the current date in Day of Week format

**cMDthYShort** gives the current date in Month day 2-digit year format

**cMDthY** gives the current date in Month Day 4-digit year format

**cHMSampm** gives the current date in h:mm:ss a format

**cHMampm** gives the current date in h:mm a format

**cHMS24** gives the current date in H:mm:ss 24 hour format

**cHM24** gives the current date in H:mm 24 hour format

**filename** gives the name of the template file. If the clipboard was expanded, then it gives nothing.

Let me know if you would like other macros!


