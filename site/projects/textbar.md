---
date: 2019-11-01
title: "TextBar"
---

## {{title}}

#### {{cdate date 'MMMM D, YYYY'}}

[Textbar](http://richsomerfield.com/apps/textbar/) is a program with the same functionality as 
[Bitbar](https://getbitbar.com/), but is being actively developed. It also has a HTML mode to
display HTML content. I moved several of my Bitbar scripts to it and created several unique
scripts. You can download the scripts [here](https://github.com/raguay/TextBarScripts).

The following is a short description of each of my scripts:

## TodoNotePlan

This is a port of my [BitBar](https://getbitbar.com/) script by the same name. It will display the current days todo items from [NotePlan](https://noteplan.co/). It works with my [Alfred NotePlan Workflow](https://github.com/raguay/MyAlfred/blob/master/Alfred%203/NotePlanWorkflow.alfredworkflow).

## TaskPaperTodo

This script displays the current days todo item in the [TaskPaper](https://www.taskpaper.com/) program for the macOS. The items are color coded based on the tags for the todos. You can edit the colors by editing the script. You have to set the file location of the **TaskPaper** file you want to use.

This script complements the [Alfred ToDo Workflow](https://github.com/raguay/MyAlfred/blob/master/Alfred%203/TodoWorkflow.alfredworkflow) in my [GitHub Alfred repository](https://github.com/raguay/MyAlfred)

This is a port of the same script for [BitBar](https://getbitbar.com/).

## Current Files and Editor

This script displays a list of often edited files and editors that you use. These are in the files: ~/.myCurrentFiles (one file per line of files you want to appear in the list), ~/.myeditorchoice (The current editor you have selected to use), and ~/.myeditors (List of editors you use. Text name with a pipe symbal and then the path to the editor).

I use the Alfred Workflow [My Editor Workflow](https://github.com/raguay/MyAlfred/blob/master/Alfred%203/My%20Editor%20Workflow.alfredworkflow) to edit and add things to these files.

## Dir Listing

This is an example of using a simple node based web server to give information to the webview in TextBar. You can browse your directories and files in the webview. It is actually very handy!

This one requires you have have node.js installed on your system. The easiest way for that is by installing it with [Homebrew](http://brew.sh).

## NotePad

This is another example of using a node based web server to give information to the url view in TextBar. This notepad application gives you 9 pages to switch back and forth for various notes. It will save the notes to a file in your home directory called `~/.notepad/.notesjson`. 

It has built-in scripts and user defined scripts that are kept in the file `~/.notepad/.scriptsjson`. You can select some text, press `<meta>-m`, select the script from the menu that pops up (the menu is scrollable to see all the scripts. It also has a search box to narrow down the selections. You can then use up and down arrows to select one.), and that script will be executed. If you don't select some text first, the script is applied to all the text in the current note. If the `insert` flag is set, it will insert the text to the cursor location. It currently has 36 scripts. Let me know if there is a script you really need!

It also has a built-in Script Editor that you can use to create your own scripts. Press `<meta>-e` and you will be given the Script Editor. Press it again, and you will be back to the notes. You save the script by pressing the `Save` button or by pressing `<meta>-s`. Saving puts you back in the notes page. You can re-edit an existing user script by pressing `<meta>-m` (yes, I'm reusing the exact same code for the script menu in the notes page). Pressing `Delete` or `<ctrl>-x` will delete the script and give you a blank script. See the section below for details on making scripts.

It now has a Regular Expression editor that will show you the results of your regular expressions, color code the sub-matches (embedded sub-matches are not supported). You can save your regular expressions and recall them by name given. You invoke the regular expression editor with `<meta>-r`. You can list the defined regular expressions with `<meta>-m`. The editor will allow you to save the regular expressions with the `Save` button and perform all the substitutions with the `Change All` button. Pressing `<meta>-r` will take you back out of the regular expressions editor. The regular expressions saved will be stored in the `~/.notepad/.regexpjson` file.

You have to have node.js installed on your system to run this script. The easiest way for that is by installing it with [Homebrew](http://brew.sh). The script is expecting node to be at `/usr/local/bin/node`.

There is a hamburger menu at the lower left corner that will open the main menu when clicked. This gives the option to: show the about dialog, open the preferences (still being worked on), option to open a help document in your browser, open the regular expression editor, open the script editor, and install the scripts for Alfred, LaunchBar, Keyboard Maestro, and Dropzone.

There is a new, larger circle on the far right. This will open the todo list manager. It currently opens the todos for NotePlan if you have that on your system. This will eventually have the option for other todo lists, but I haven't integrated it yet.

Also, you can use TeaCode to expand snippets if you have it installed on your system. Just highlight the snippet and press `<ctrl><shift>e`. In a notepad, it will be expaned as a file with an extension of 'md'. In the script editor, it will be expanded as a file with the extension of 'js'.

More features to come. Stay tuned!


### Math Features

The notepads now have scripts for processing math: the 'Basic Math' and 'Evaluate Page for Math' scripts. The 'Basic Math' script is for processing arbitrary pieces of math in a selection. The 'Evaluate Page for Math' script is for processing the entire note with a nice running result along the right. The 'Basic Math' script doesn't reset the state of the math library (ie: variable definitions and functions), but the 'Evaluate Page for Math' does each time invoked so as to not create multiple copies of function and variables.

Copy the following note to a notepad:

```markdown
# Using the âEvaluate Page for Mathâ script

Your notes can have any text you need. But when a line starts with a â>â, that whole line is processed for math. The line is processed and the answer pushed to the right with a â|â symbol.

> 6 * 95
> x=6*8-10
> x

Text in the middle doesnât clear out the variable or function assignments before it.

> f(x)=x^2-5*x+12
> f(60)
> f(x)

The length of the note isnât a concern either.

> f(100)

> bank=34675
> check=5067
> balance = bank - check

> sin(45)

The math package used doesnât do conversions or symbols inside of the math expressions. The math library used is [mathjs 4.0](http://mathjs.org/).
```

Then press `<ctrl>-m` and select the 'Evaluate Page for Math' script. Each line with the '>' as the front character now has the results to the right. When you change the text lines and re-run the script, the math lines are all updated. All other lines are not effected by the script. You can change any equation or variable and it's effects will trickle down the page.

### Making Scripts

All scripts have to get the text to process from `NP.text` and place the new text back into the `NP.text` variable. For example, in a note, place the following code:

```javascript
try {
   var lines = NP.text.split('\n');
  NP.text = '';
  for(var i = 0; i < lines.length ; i++) {
      var match = lines[i].trim().match(/^\d+\. (.*)$/);
    if (match != null)
        NP.text += match[1] + '\n';
  }
} catch (e) {
   NP.text += "\n\n" + e.toString()
}
```

Then go to a different note and place several lines of text. Run the script `Bullet lines with Numbers`. Every line will have the proper number at the front of it. Now, run the script `Evaluate Note # as Script` with `#` the number of the note you put the script. The numbers at the beginning will now be removed!

You can access the following libraries also: `NP.moment` for [moment.js library](https://momentjs.com/), `NP.mathjs` for the [math.js library](http://mathjs.org/), and `NP.jQuery` for the [jQuery.js library](https://jquery.com/).

### Features that have been added or fixed

- Added security to the server. Only tcp points from the same computer can use private API. Only local sub-domain can use the public API.
- Fixed: removed white boarder and it now doesn't try to scroll.
- Fixed: Launcher code more consistent and less buggy.
- History is now remembered and maintained on a per note basis while running.
- Server API for outside programs to work with notes.
- Server to browser connection to update notes.
- Move server to an express server with socketIO.
- Start-up now shows the first note properly.
- Cursor position is remembered and set back when changing notes.
- Improved menu colors to match the current color scheme better.
- Now the backend is a full express server that will allow more types of interaction than before.
- Fix the XML errors when saving notes to the server.
- Cursor is placed back to the position it was before leaving a note.
- Fixed: Undoing after changing notes puts all the notes from the last note into the current note. Need to clear out the undo buffer when changing notes.
- Storing regular expressions with a meaningful name for future use.
- Regular expressions selecting and editing of notes.
- Editing and adding new scripts.
- Add new scripts without having to remove the script store.
- It will now come up showing the first note without having to press the bottom button.
- When you change notes, the text area will get input focus right away without having to click on it.
- Cursor now is set to the end of the area changed by a script.
- Math features have been added using the math.js library.
- Added many time and date based scripts using moment.js library.
- Scripts that work on the whole note or just the selection.
- Pop-up menu of available scripts with an input for condensing the number of items by only showing script names with the letters typed in it. Then you use the up/down arrows to select one and `enter` to run the script. Or, you can scroll and click the desired one.
- A hotkey (ctrl-s) to stop the node.js server.
- Full text editor support with color highlighting (markdown) and my own theme.
- Re-factored to use the [CodeMirror](https://codemirror.net) editor instead of a plain textarea.
- The script menu now has a focused input to narrow down the list with text given. Then you can use the up and down arrow keys to select the script you want to use.
- You can now write a script in a note, switch to another not and select some text, and run the 'Evaluate Note # as a Script' where # is 1-5. The selected text is in `NP.text`. You can access the following libraries also: `NP.moment` for moment.js library, `NP.mathjs` for the math.js library, and `NP.jQuery` for the jQuery.js library. These things can change as I work to make this a better program.

{{> 'donate.html'}}
