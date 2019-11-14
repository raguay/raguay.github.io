---
title: LaunchBar Actions
date: 2018-11-15 18:00:57
---
## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}


[LaunchBar 6](http://www.obdev.at/) is an application similar to Alfred. Since I love making scripts and extensions, I naturally started making some for LaunchBar as well. I also had many requests for porting some of my Alfred workflows to LaunchBar. Therefore, this is the results. If you have a particular need, let me know.

You can find all of these actions on my [GitHub account](https://github.com/raguay/MyLaunchBarActions).

Evaluate JavaScript
---

This handy action is a good way to test JavaScript; especially, LaunchBar specific JavaScript. Once you have this action installed, simply highlight some JavaScript code, press and hold the key sequence for your LaunchBar. When LaunchBar shows up with the text, send the text to the action. For example, highlight and run this snippet:

```javascript
    LaunchBar.displayInLargeType({
        title: 'Don’t you just hate this font?',
        string: 'You should.',
        font: 'Comic Sans MS'
    });
```

When you send it to this action, a large type display in Comic Sans will ask you if you hate this font.

To Buddhist Year
---

This action will convert the current date to the Buddhist calendar and display it in a notification. If a date string is passed, it will convert it to the Buddhist calendar and display it in a notification. The Buddhist date is also copied to the clipboard for easy insertion into a document.

List Processor and List Processor - Options
---

These two actions work together. The List Processor - Options allows you to set the different options for the action. The separator is a character that you want to use to separate the list into different parts. The position is the location in the list for the next retrieval. The forward options tells if the next call will progress forwards in the list or backwards.

By quick sending (cmd-space held until the selection is copied into LaunchBar. Then press tab.) to the List Processor action, you can set the string to be processed. Then just run the List Processor action without a string gets the next item in the list.

This is very handy for sequencing through a list of items.

Add To TaskPaper Projects
---

This action is used to add a new task to a [TaskPaper](https://www.taskpaper.com/) project. If you send a path of a TaskPaper file to this action, it stores that path to add tasks to. Otherwise, if **TaskPaper** is running while you run this action, it will get that files path, store it, and use that file.

Once it has determined what file to use, it asks the user for the task line and which project to add it to. The user simply types the name of the task, and selects the project. That new task will be added to the top of that project.


Paste Through TextExpander
---

This action accepts a string. That string is past to **[TextExpander](https://smilesoftware.com/textexpander)** for pasting into the top most application and expanding it's specific macros. This action is used by the **Quiver Snippets** action to paste the snippets through **TextExpander**.

Quiver Snippets
---

This action allows you to create and manage snippets in the **[Quiver](http://happenapps.com/#quiver)** application. When you load the action, send either your Quiver Library file or a shared Snippets notebook file to the action. That will configure the action and give you the option of loaded the Default note and the sample snippets. It also allows you to load the help files in to **Quiver**. Please refer to the help file for more information.

Quick Load and Quick Load Options
---

This action finds the most recently modified/created file in the Downloads directory and loads it into LaunchBar. You can the action it with any program you want. If you want a different directory, simply change the name of the directory in the user's home directory in the variable "searchDir".

The Quick Load Options allow you to change the directory being searched by sending a new directory to this action. By running the action (Abbreviation is set to 'lop'), you can set the sort type (by last modified or by last added to the directory) and the order number (Most recent, second most recent, etc.). If you set it to the 5th most recent, but there are only two items, it will correctly get the last item.

The Quick Load action uses the users Download directory, first most recent file, and sort by last modified as the defaults.


DockShelf.app
---

[DockShelf](http://www.thealchemistguild.com/dockshelf/) is a great dock replacement program for Mac OS X. The following actions are for this program:

**DockShelfWorkspaces.lbaction**

This action has an abbreviation set to `dsws` to show a list of workspaces defined. When you select one, **DockShelf** will switch to that workspace.

FoldingText.app
---

[FoldingText](http://foldingtext.com) is a great markdown editor. It is easily extendable with scripts and extensions. Here, I have the LaunchBar scripts that I use with FoldingText.

**FoldingText.lbaction**

This is a collection of quick scripts for performing different actions. You type the keyword **ft-action** that will list all the possible actions. As you type a title, the list will shorten to the one you want. The possible actions are:

- **FoldingText Documents** - a list of available documents about FoldingText.
- **Open Selection** - Will take the currently selected file in either **Finder** or **PathFinder** and open it in FoldingText.
- **Get Visible Text** - All non-folded text will be copied to the clipboard.
- **Chrome Tabs** - A link to each tab in the topmost Chrome browser will be listed in the topmost FoldingText document at the current location.
- **Safari Tabs** - A link to each tab in the topmost Safari browser will be listed in the topmost FoldingText document at the current location.
- **Remove Tags** - Will give a list of the tags in the topmost FoldingText document and remove the tags you select.
- **Marked** - Opens the topmost FoldingText document in **[Marked 2.app](http://marked2app.com/)**.
- **Next** - This will find the first @next tag in the document, change it to done with the current date and time, and move the @next tag to the next item.

**FoldingTextAddToTag.lbaction**

This action is triggered with **ft-addtotag**. When triggered, you can type anything and have that added to the tag you select from a list of tags obtained from the topmost document. Therefore, if you topmost document has a @inbox tag, it will list it for you to add a new item.

**FoldingTextBookMarks.lbaction**

This action is triggered by **ft-bookmark**. It will prompt you with a list of actions: **go to bookmark**, **make bookmark**, **remove bookmard**, or **install bookmark activator**.

The **make-bookmark** requires you to add a text to set as the title for the bookmark. Therefore, type **mark|This is my title** will get the current location in the topmost FoldingText document and remember it with the title **This is my title**. The **|** tells the script that the next item is the title. The **make-bookmark** also lease the URI in the clipboard.

The **get-bookmark-UIR** will simple get the URI for the current location in the current FoldingText document and place it in the clipboard. You can then paste it in to another application or document. Great for making jump to lists.

In order to go to a bookmark, the **bookmark activator** has to be ran at least once on your system. This will add a special URI handler for FoldingText bookmarks.

**FoldingTextGoToTag.lbaction**

This action is triggered with **ft-gototag**. It will show a list of tags from the topmost document. You select the one you want focused.

**FoldingTextInbox.lbaction**

This action is triggered with **ft-inbox**. It allows you to type any text and have it appended to the bottom of that tag. Therefore, if you have a todo list with a tag of @inbox, you can type **- I need to do this** and it will be added to the todo list properly.

##### Tutorials

- [Creating LaunchBar 6 Actions](http://computers.tutsplus.com/tutorials/creating-launchbar-6-actions--cms-22733)

{{> 'donate.html'}}
