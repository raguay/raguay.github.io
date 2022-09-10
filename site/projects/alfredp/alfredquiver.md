---
title: Quiver Workflow
date: 2018-11-12 12:55:32
---
## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}


This workflow allows you to create templates with Handlebar syntax inside of the **[Quiver](http://happenapps.com/#quiver)** program. To use the workflow, you have to have Node.js installed first. I recommend using **[Homebrew](http://brew.io)** to install it.

Once **Node.js** is installed, go to your Quiver Library file in Alfred Browser and select the “**Set Quiver Library**” file action. This tells the workflow where your templates (or snippets) are to be kept. Create a workbook called “Snippets” with one note called Defaults. The Defaults note has to have one code block set to JSON and the defaults for the Handlebar expansions set. The rest of the notes will be templates.

When you run “**qt:expand**” or “**qt:exptext**”, it will list all of your template files in the Snippets notebook. When you select one, it will be expanded with any json cell the note and the Defaults json note data. The “**qt:expand**” will put the result into your clipboard and the topmost application. The “**qt:exptext**” will give it to TextExpander to expand and place in the topmost application. With the “**qt:exptext**” command, TextExpander will also expand any of it’s macros in the template file. I mostly use it for placing the cursor after expansion. These two commands also have an associated Alfred Browser File action.

There are four special helper function for Handlebars defined. These functions should be placed inside double or triple brackets. They are:

**save &lt;name&gt; &lt;text&gt;**
This command creates a helper named “&lt;name&gt;” with the expanding text of “&lt;text&gt;”. It also places the given “&lt;text&gt;” at the point of definition. This allows you to create text snippets on the fly inside the template. Very handy.

**clipboard**
This helper command places the current clipboard contents at the point in the template.

**date &lt;format&gt;**
This will format the current date and time as per the format string given. See the help document that is loaded upon initialization.

**cdate &lt;date/time&gt; &lt;format&gt;**
This takes the date/time string and formats it according to the format given.  See the help document that is loaded upon initialization.


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

There is more to come!

