---
date: 2020-02-03
title: Create a Local Plash Server Using Svelte - Setup and Beginning Files
---

# {{title}}

#### {{cdate date 'MMMM D, YYYY'}}

When I saw [Plash](https://sindresorhus.com/plash), I knew I wanted it. Plash 
allows you to set any website url as your background on a macOS computer. But, 
it requires you to update to Catalina since it's only available for that version. 
I was very reluntant to upgrade due to the lack of support for 32-bit apps (which 
I still had some). I've used other programs that were similar to Plash, but they 
all had issues with some sites and some scripts. I finally upgraded and downloaded 
Plash. Plash works great, but I wanted more than a static picture background. So, 
I decided to make my own desktop site to load into Plash. 

[Svelte](https://svelte.dev) is my preferred JavaScript framework. It creates 
fast JavaScript applications with minimal size due to being a transpiler and not 
a library of functions. I've created my [website](http://customct.com) using 
Svelte and markdown files on GitHub. You can follow that project in my 
tutorial [Using the Svelte GitHub Website Template](http://www.customct.com/#/tutorials/svelteweb/using-template). 

## Getting Started

In order to run with Svelte, you have to have node and npm installed. On the 
Mac, I prefer installing from [Homebrew](https://brew.sh). That way, you can 
update many programs at once with `brew update` command line. As of this 
writing, I'm using Homebrew version 2.4 on Catalina with [node.js](https://nodejs.org/en/) 
version 12.12.

With node installed, create your project directory and enter into it. I'm calling 
the project `SveltePlashServer`. In that directory, run this command line:

```sh
npx degit sveltejs/template UI
```

Then enter the `UI` directory and run the following commands:

```sh
npm install
npm run dev
```

With this you will have Svelte installed and running in a development server on the 
project. When you add or edit any file in the project `src` directory, the project 
will rebuild and reloaded into the web browser. You can open a web browser to 
`http://localhost:5000` and see the current project. Or, you can go ahead an use 
Plash to view it on the background.

Just click on the Plash menubar icon and select `Open URL...`. In the dialog, type 
in the address `http://localhost:5000`. The same screen seen in your browser will now 
be the background of your Mac! As you edit the source files, that background will 
update as well. If you want to see the background completely, click on `Browsing Mode` 
in the Plash menubar menu and the background will now be in the foreground. Remember, 
you can't enteract with other programs with Plash in `Browsing Mode`.

With the full development environment setup now, we can start diving into the 
actual code!

## Stores

In the `src` directory, create the following directories: `store`, and `components`. 
The `store` directory will contain all the stores we will be using. The `components` 
directory is for our components. You can just remove the `main.js` file and the `App.svelte` 
file from the Svelte install. We will be creating our own in the next section.

Moving into the `store` directory, create a file called `secondStore.js` and 
`thirtyMinuteStore.js`. These will be our seconds timer and thirty minute timer for 
updating the background. These stores will function just like [Rx.js](https://rxjs-dev.firebaseapp.com/) 
observables. In fact, I had a hard time understanding Svelte stores until I started 
thinking of them in this manner. As you will see in the `UI.svelte` file (the file 
to replace the `App.svelte` file), I'm updating these stores based on a timer. Any 
component that subscribes to them will be notified every second or thirty minutes. 

In the `secondStore.js` file, place this code:

```JavaScript
import { writable } from 'svelte/store';

export const Seconds = writable({
  hours: 0,
  minutes: 0
});

```

The second store will be updated every minute with the current hour and minute time. 
It is a `writable` store since it will be containing the current time that is updated. 
Any component can subscribe to it in order to get the current time. We will be using 
this in two of our main components.

In the `thirtyMinuteStore.js` file, place this code:

```JavaScript
import { writable } from 'svelte/store';

export const thirtyMinute = writable(0);
```

This store simply has a counter that will increment every thirty minutes. This 
is the simplest store you can write. But, as you can see, the timing logic isn't 
in the stores. That logic is in the main application file `UI.svelte`.

## The Main Files

In Svelte, there are two main files and then component and store files. The two 
main files are `main.js` and `UI.svelte`. The `main.js` sets up the configuration 
for the application and starts the Svelte main component. The `UI.sevelte` file is 
the main component for this application.

In the `main.js` file, place this code:

```JavaScript
import UI from './UI.svelte';
import Time from './components/Time.svelte';
import CircleTime from './components/CircleTime.svelte';

//
// Create the configuration and widgets structures for configuring
// the desktop. This is the only area the user should have to change.
// Well, other than creating new widgets!
//
const widgets = [{
  name: 'Time',
  widget: Time,
  top: 145,
  left: 35,
  style: {
    font: 'Alfa Slab One',
    size: 40,
    color: 'white'
  },
  config: {
    shadow: '1px 1px 0px black, 2px 2px 0px black, 3px 3px 0px black, 4px 4px 0px black, 5px 5px 0px black, 6px 6px 2px black'
  }
}, {
  name: 'CircleTime',
  widget: CircleTime,
  top: 20,
  left: 50,
  style: {
    font: 'Arial',
    size: 500,
    color: 'white'
  },
  config: {
    radius: 80,
    lineWidth: 10,
    strokeStyleMin: 'blue',
    strokeStyleHour: 'green',
    gap: 10
  }
}];

const config = {
  backgroundType: 'pic',
  backgrounds: ['https://source.unsplash.com/random/1440x900?puppy', 
                'https://source.unsplash.com/random/1440x900?kitten',
                'https://source.unsplash.com/random/1440x900?glider',
                'https://source.unsplash.com/random/1440x900?galaxy',
                'http://www.talencia.cat/mypics/max/1/16113_stars-backgrounds.png'],
  backgroundColors: ['background: linear-gradient(to left top, blue, red) fixed',
                     'background-color: teal',
                     'background-color: lightblue',
                     'background: linear-gradient(to right top, teal, lightgreen)',
                     'background-color: #08AEEA; background-image: linear-gradient(0deg, #08AEEA 0%, #2AF598 100%)',
                     'background-color: #21D4FD; background-image: linear-gradient(19deg, #21D4FD 0%, #B721FF 100%)',
                     'background-color: #8EC5FC; background-image: linear-gradient(62deg, #8EC5FC 0%, #E0C3FC 100%)',
                     'background: linear-gradient(to left top, blue, lightgreen)'],
  random: true,
  index: 0,
  randomAll: true,
  update30: true
};

const ui = new UI({
  target: document.body,
  props: {
    widgets: widgets,
    config: config
  }
});

export default ui;
```

The first part of this file is loading in the different components to make up 
the background for Plash. We are loading them here to place them in the configuration 
structure for creating the desktop environment. You will see how we use them in the 
`Desktop.svelte` component latter on.

After the importing of the components, I am creating two structures: `widgets` and 
`config`. The `widgets` structure is an array of objects describing the various 
widgets we will be using to create the background. Here, we are using the `Time` 
and `CircleTime` components. Each widget object contains the position of the widget, 
an instance of a component widget, a styling object for the widget, and a 
configuration for that widget. 

The `config` object holds configuration information for the full application. This 
configuration is mostly used by the `Desktop.svelte` component to control the 
"background" of the desktop component. This component will enable us to have random 
backgrounds that update on the thirty minute intraval.

The last part of the `main.js` file in the creating the `UI.svelte` component instance 
and passing the `widget` and `config` objects as `props` or properties of the component. 
This is how a Svelte component is created in pure JavaScript. We are passing the body 
of the document for creating the Svelte target. This will make the Svelte component the 
entire HTML document that is seen. The `ui` object created is the given as the default 
export in case the file is loaded as a object in another program.

## The `UI.svelte` Component

Next, in the `UI.svelte` file I will be showing pieces of it at a time and
explaining what that part of it does. This file is larger than the others and
merrits some explanations. So, let's start with the top:

```html
<svelte:head>
  <link href="https://fonts.googleapis.com/css?family=Alfa+Slab+One&display=swap" rel="stylesheet">
</svelte:head>
```

This tells Svelte to place the line into the header of the website. This is idea
for adding google fonts that I want to use for the time display. Here, I'm
loading the `Alfa Slab One` font which is a nice, block form font. I will be
using it in the `Time.svelte` component.

```html
<Desktop config={config} >
  {#each widgets as widget}
    <svelte:component 
      this={widget.widget} 
      top={widget.top}
      left={widget.left}
      style={widget.style}
      config={widget.config}
    />
  {/each}
</Desktop>
```

This is the template for the component. In the template, I'm using the
`Desktop.svelte` component to create the whole desktop. I'm passing the `config`
structure to the desktop to configure it.

This shows a neat feature of Svelte. You can encompass anything inside the
component tags. Those items are passed to the component as a slot. I could use
named slots, but I don't have more than one area in the current design. Maybe
down the road....

Inside of the Desktop component, I'm looping over the widgets to create an
instance of each widget. The `{#each }{/each}` directive performs the looping.
Inside the loop, I'm using the `<svelte:component ...>` to create an instance of
the new component from what the `widgets` array gives in the `main.js` file. The
`this=...` sets the JavaScript object that will instantiate the component. The
rest are parameters passed to the component. Therefore, all widgets in the
Desktop must accept the `top`, `left`, `style`, and `config` parameters.



```html
<style>
  :global(body) {
    width: 100%;
    height: 100%;
  }
</style>
```

Next, we have the CSS styling for this component. Not much, just setting the
body width and height to take up all the available space. In order to give a
global style, you have to prefix the item for it with the `:global()` directive.
This tells Svelte to take this styling and make it global for that item. Here,
it is styling for the `body` element. This is necessary since component styling
is created for each instance of a component individually.

The next section is the script tag with all the JavaScript for the component.
Since there is a lot here, I'll go over each bit of it so that you will
understand what is going on. 

```html
<script>
  import {onMount} from 'svelte';
  import { Seconds } from './store/secondStore.js';
  import { thirtyMinute } from './store/thirtyMinuteStore.js';
  import Desktop from './components/Desktop.svelte';
```

This first section are the imports. Here, I'm importing the Desktop component
  and the two Svelte stores. I'm also importing `onMount`. This is a life cycle
  hook for Svelte. You give it a function that is ran after the component is
  mounted. Your function should return a function to be ran when the component
  in unmounted.

```javascript
  export let widgets = [];
  export let config = {};
  
  let thirtyCount = 0;
```
Next, I'm creating the variables for each property the component is expected the
  caller to pass to it. Here, the `widgets` and `config` properties are defined
  and initialized to an empty array and object. I'm also creating the
  `thirtyCount` variable to count down how many thirty minute clock ticks have
  gone by.
  
```javascript
  onMount(() => {
    UpdateTimeSeconds();
    UpdateTimeThirtyMinutes();
    return(() => {
    });
  });
```

Next, I'm using the `onMount()` life cycle function to set the function to run
when the component is mounted. This function will start the two timers. It is
returning a empty function since there isn't any teardown needed. I should stop
the timers when it is unmounted, but really, this would never happen as it will
be running until the Plash program is stopped. Therefore, it doesn't really matter.

```JavaScript

  function UpdateTimeSeconds() {
      //
      // Set the new date in the seconds store for everyone to
      // use.
      //
      var ct = new Date();
      Seconds.set({
        hours: ct.getHours(),
        minutes: ct.getMinutes()
      });
      setTimeout(UpdateTimeSeconds, 1000);
  }

  function UpdateTimeThirtyMinutes() {
      thirtyCount += 1;
      thirtyMinute.set(thirtyCount);
      setTimeout(UpdateTimeThirtyMinutes, 30*60*1000);
  }
</script>
```
The last two function are the ones for setting up and keeping the one second and
thirty minute timers going. The one second timer also gets the current time and
stores it in the store. This will be used to display the current time. I'm using
a counter variable to set a new thirty minute timer. This is quicker than
getting the current store value, incrementing it, and then setting it. The value
isn't important. It just needs to be different in order for the other
subscriptions to the store to get notified of a change. If the value doesn't
change, the store isn't updated and no other component will know that the timer
had changed.

## The `Desktop.svelte` Component

The Desktop component controls the background image and the placement of the
widgets. It could also be use to place special controls to control the behaviour
of the system. We will explore that in a different tutorial. For now, create the
`Desktop.svelte` file in the `components` directory. In that file, place the
following lines:

```html
<div id='Desktop' style="{background};">
  <slot>
  </slot>
</div>
```

This template is very simple. It is a single `div` with an id of `Desktop` and a
style set by the `background` Svelte variable. Inside the `div`, you see the
markup for the un-named slot. This is where all the widgets will be placed from
the UI component definition. 

```html
<style>
  #Desktop {
    display: inline;
    position: absolute;
    top: 0px;
    left: 0px;
    width: 100%;
    height: 100%;
  }
</style>
```

The styling for the Desktop is also very simple. Make it as larage as possible
with absolute placement starting at the topmost left position.

```javascript
<script>
  import { onMount } from 'svelte';
  import { thirtyMinute } from '../store/thirtyMinuteStore.js';

  export let config;

  let background;
  let lastType;
```

As before, I'm importing the thirtyMinute timer and the `onMount` command from
Svelte. I'll be using the timer to change the background every thirty minutes.
I'm also declaring the `config` property to be filled by the component that
calls it. I'm using two component variables: `background` for controling the
background style for the `div`, and `lastType` to keep track of the last type
of background used.

```javascript
$: background = setBackground(config);
```

This line might look a little strange. This is how you mark a variable change as
reactive. The `$:` tells Svelte to update the template whenever a variable
referenced on this line changes. Therefore, if the `config` file changes the
`setBackground()` function will be called with `config` and the results placed
in the `background` variable. That will trigger the `div` to be updated with the
new styling.

```javascript 
function setBackground(config) {
  var result = '';
  var types = ['pic', 'solid', 'none'];
  var usetype = config.backgroundType;
  if(config.randomAll) {
    do {
      usetype = types[(Math.floor(types.length*Math.random()))];
    } while(lastType === usetype);
    lastType = usetype;
  }

  switch(usetype) {
    case 'pic': 
      var index = config.index;
      if(config.random) {
        //
        // Get a random index for the number of images.
        //
        index = Math.floor(config.backgrounds.length*Math.random());
      }
        
      //
      // Set the background to that image.
      //
      result = 'background-image: url(\'' + config.backgrounds[index] + '\'); background-repeat: no-repeat; background-size: cover';
      break;

    case 'solid':
      var index = config.index;
      if(config.random) {
        index = Math.floor(config.backgroundColors.length*Math.random());
      }
      result = config.backgroundColors[index];
      break;
       
    case 'none':
    default:
      result = '';
  }
  return(result);
}
```

The `setBackground()` function is responcible for setting the `background`
variable to the correct value for displaying the different types of
background. There are three types of background: `pic` which is a picture
obtained from the net (We will look into expanding that to local files in a
future tutorial), `color` which will set the background to a color or gradiant
fill, or `none` which will leave the background transparent and the user will
set the background set by the operating system.
  
The configuration for the `Desktop` component allows the user to set a random
item for each type (which has no meaning for `none`), and to use random types
of backgrounds as well. When using random types of backgrounds, the `lastType`
variable is checked to see if the new random one is the same. A new random
value will be generated until it doesn't match the `lastType`.

```javascript
  onMount(() => {
    const unsubscribeThirtyMinute = thirtyMinute.subscribe((value) => {
      if(config.update30) {
        background = setBackground(config);
      }
    });
    return(() => {
      unsubscribeThirtyMinute();
    });
  });
</script>
```

The last thing in the file is the `onMount()` function call. Here, I'm
subscribing to the `thirtyMinute` store. Whenever the store is updated, it will
call the `setBackground()` function to set the new background. It also returns
a function to unsubscript to the `thrityMinute` store.

That is all of the supporting components. The widgets are next to be created.

## The `CircleMeter.svelte` Component Widget

The `CircleMeter` component is used to show a circle outline based on
percentage. At one percent, just a dot of the circle outline will be shown. At
thirty percent, half the circle. And at 100 percent, the whole circle will be
shown. This will be used in the `CircleTime` component.

Create the `CircleMeter.svelte` file in the `components` directory and begin
filling with the following code:

```html
<canvas 
  bind:this={arcCanvas}
  width="{config.width}" 
  height="{config.height}"
  style="top: {top}px; left: {left}px; font-family: {style.font};"
>
  <p>Your browser does not support the HTML5 canvas tag.</p>
</canvas>
```

The template consists of a single `canvas` element. The `width` and `height`
properties are set from the corresponding values in the `config` parameter
variable. The `style` property is set from both the `config` and `style`
parameter variables. The one new item in this template is the
`bind:this={arcCanvas}`. This directive in Svelte will bind the canvas element
to the varaiable `arcCanvas` which is then used in function to manipulate the
canvas. Gone are the days that you had to use `document.getElementById()`! This
is much cleaner way to do it.

```html
<style>
  canvas {
    position: absolute;
  }
</style>
```

The styling is simple. Make sure it can be positioned absolutely.

```javascript
<script>
  export let top;
  export let left;
  export let style;
  export let config;
  export let percent;
  
  let arcCanvas;
  let ctx = null;
 ```
 
 This is the standard defining of parameters and component variables. `top`,
  `left`, `style`, and `config` are for the `top`, `left`, `style`, and `config`
  parameters passed to the component. The `percent` is also a parameter passed
  in. This variable will set how much of the circle to show. It is the main
  reactive element in the component.
  
  The `arcCanvas` is set by the `bind:this` directive in the `canvas` element.
  The `ctx` variable is used to create context to manipulate the canvas.
  
 ``` 
  $: (percent !== 'undefined')&&(percent !== 0) ? drawCanvas(percent) : 1;
 ```
 
 Again, I have a reactive line. This one simply calls the `drawCanvas()`
  function only when the passed value of `percent` is a valid value to use. This
  guards from a division by zero and allows a function to be called when the
  parameter changes.

 ```javascript
  function clearCanvas(context) {
    // Store the current transformation matrix
    context.save();

    // Use the identity matrix while clearing the canvas
    context.setTransform(1, 0, 0, 1, 0, 0);
    context.clearRect(0, 0, config.width, config.height);

    // Restore the transform
    context.restore();
  }
 ```
 
 The `clearCanvas()` function does exactly what it says. It is used to clear the
  canvas before writing a new circle. Since the canvas uses a rotation to make
  the beginning of it to be at the top, you have to temperary clear the rotation
  before using the `clearRect()` function. The calls to `save()` and `restore()`
  keeps the original rotation in place.
  
 ```javascript
  function drawCanvas(percent) {
    if((typeof arcCanvas !== 'undefined')&&(arcCanvas !== null)) {
      var rad1 = (config.height/2);
      var rad2 = (config.height/2)-(config.lineWidth/2);
      if(ctx === null) {
        //
        // Setup the canvas.
        //
        ctx = arcCanvas.getContext("2d");
        ctx.lineWidth = config.lineWidth;
        ctx.strokeStyle = config.strokeStyle;
        ctx.beginPath();

        //
        // Translate the matrix to put the start of the circle
        // at the top.
        //
        ctx.translate(rad1,rad1);
        ctx.rotate(-Math.PI/2);
        ctx.translate(-rad1,-rad1);

        //
        // draw the circle.
        //
        ctx.lineCap = "round";
        ctx.arc(rad1, rad1, rad2, 0, (2 * (percent/100)) * Math.PI);
        ctx.stroke();
      } else {
        //
        // draw the circle after clearing the canvas.
        //
        ctx.beginPath();
        clearCanvas(ctx);
        ctx.arc(rad1, rad1, rad2, 0, (2 * (percent/100)) * Math.PI);
        ctx.stroke();
      }
    }
  }
</script> 
```

The last function, `drawCanvas()` does all the work. If the context for the 2D
graphics haven't been created yet, it creates it with the proper rotation. If it
has, it clears the circle and draws the arc while saving and preserving the rotation.

## The `CircleTime.svelte` Component

Now that we have a `CircleMeter.svelte` component, we can use it to create the 
current time in a semi-circle format. I really like the way that looks on the 
screen. Create the `CircleTime.svelte` file in the components directory and 
start adding the code:

```html
<div id='CircleTime' style="top: {top}px; left: {left}px;">
  <CircleMeter 
    top=0
    left=0
    style={style}
    config={hourConfig}
    percent={hourPercent}
  />
  <CircleMeter 
    top={innerTop}
    left={innerLeft}
    style={style}
    config={minConfig}
    percent={minPercent}
  />
</div>
```

The first section, as always, is the template. This one is a contain `div` 
element with two `CircleMeter` components defined. Their placement the hour 
circle is absolutely the whole area. The minute circle is adjusted by the 
`innerTop` and `innerLeft` component variables. Each circle has it's own 
config and percent properties: `hourConfig`, `hourPercent`, `minConfig`, 
and `minPercent`. They all make use of the same `style` configuration.

```html
<style>
  #CircleTime {
    position: absolute;
  }
</style>
```

The styling is simply making the `div` element have absolute placement. 

```javascript
<script>
  import { onMount } from 'svelte';
  import { Seconds } from '../store/secondStore.js';
  import CircleMeter from './CircleMeter.svelte';

  export let top;
  export let left;
  export let style;
  export let config;

  let minPercent;
  let hourPercent;
  let innerTop = config.lineWidth+(config.gap/2);
  let innerLeft = config.lineWidth+(config.gap/2);
  let hours = 1;
  let minutes = 1;
  
  let minConfig = {
    width: config.radius*2-(config.lineWidth*2+config.gap),
    height: config.radius*2-(config.lineWidth*2+config.gap),
    lineWidth: config.lineWidth,
    strokeStyle: config.strokeStyleMin
  };
  let hourConfig = {
    width: config.radius*2,
    height: config.radius*2,
    lineWidth: config.lineWidth,
    strokeStyle: config.strokeStyleHour
  };
 ```

The imports are getting the `onMount` life cycle command, the `CircleMeter` and 
`Seconds` Svelte store. The `minPercent` and `hourPercent` are left uninitialized. 
But, I'm setting the `innerTop` and `innerLeft` variables to the `config.lineWidth` 
plus half of the `config.gap` size. This should place the top left corner just 
inside the hour circle. The `hours` and `minutes` are preset to 1 to keep from 
having some bad math at startup.

The two configurations for the hour and minute circles are taking into account 
that the minute circle is inside the hour circle. Also, their corresponding line 
styles are applied.

 ```javascript
  onMount(() => {
    var unsubscribeSeconds = Seconds.subscribe((value)=>{
      hours = Number(value.hours);
      minutes = Number(value.minutes);
      calPercent();
    });
    var dt = new Date();
    minutes = Number(dt.getMinutes());
    hours = Number(dt.getHours());
    calPercent();
    return(() => {
      unsubscribeSeconds();
    });
  });
```

The `onMount` function creates a subscription to the `Seconds` store to get the 
current time. It takes the current time, sets them to the component variables, 
and calls the `calPercent()` function. After the subscription, it gets the 
current time and sets it up the same way. This keeps from having something 
bogus until the first second. It then returns a function that unsubscribes the 
`Seconds` store.

```javascript
  function calPercent() {
    if(hours > 12.0) {
      hours = hours - 12.0;
    }
    if(minutes === 0) minutes = 60.0;
    if(hours === 0) hours = 12.0;
    minPercent = (minutes/60.0) * 100.0;
    hourPercent = (hours/12.0) * 100.0;
  }
</script>
```

The `calPercent()` function will keep the time to a 12 hour segment and calculate 
the percentage of the circle that will be taken up by that time. When the `minPercent` 
and `hourPercent` variables are set, that will propagate to the `CircleMeter` 
component and it will update the graphics.

## The `Time.svelte` Component

The last widget to create for this tutorial is the `Time.svelte` component. Create 
the file and start filling it with the following:

```html
<div id='Time' style="top: {top}px; 
                      left: {left}px;" 
>
  <p
    style="text-shadow: {config.shadow};
           font-family: '{style.font}'; 
           font-size: {style.size}px; 
           color: {style.color};"
  >{zhours}:{zminutes} {ampm}</p>
</div>
```

The first section is the template that will set the location of the time in 
the `div` element. The `p` element will get the text shadow, font family, 
font size, and text color from the `config` and `style` structures passed to it. 
The inside of the `p` element has the displayable `zhours`, `zminutes`, and `ampm` 
component variables. 

```html
<style>
  #Time {
    position: absolute;
    font-weight: bold;
  }
</style>
```

The styling is the basic position absolute which is in each widget. Here, we 
add the `font-weight` to bold because a bold weight looks good on the screen. 

```javascript
<script>
  import { onMount } from 'svelte';
  import { Seconds } from '../store/secondStore.js'

  export let top;
  export let left;
  export let style;
  export let config;
  
  let hours = 12;
  let zhours = '12';
  let minutes = 0;
  let zminutes = '00';
  let ampm = "am";
```

Once again, we have the initialization of the component variables and importing 
of the `Seconds` store and the `onMount()` life cycle function.

```JavaScript
  onMount(() => {
    var unsubscribeSeconds = Seconds.subscribe((value)=>{
      hours = Number(value.hours);
      minutes = Number(value.minutes);
      if(hours > 12) {
        hours = hours - 12;
        ampm = "pm";
      } else {
        ampm = "am";
      }
      if(minutes < 10) {
        zminutes = '0' + minutes.toString();
      } else {
        zminutes = minutes.toString();
      }
      if(hours === 0) hours = 12;
      zhours = hours.toString();
    });
    return(() => {
      unsubscribeSeconds();
    });
  });
</script>
```

The `onMount()` function subscribes to the `Seconds` store to get the current time 
and it's updates. Each time it updates, it creates a zero front padding for the 
minutes display number and a 12 hour value for the hours with a proper setting 
of the `ampm` variable. I had to make sure that a zero hours is set to 12 for 
proper display and calculations of the percentage.

## Building the Desktop UI

Once you have all these files in place, you can run this command on the command 
line in the `UI` directory:

```bash
npm run build
```

This will create the `public` folder with all the files needed to display the 
desktop UI in a web browser using a web server. You could just startup a server 
using:

```bash
npm run dev
```

And a local server will be running on port 5000 of your local host. Then you would 
give Plash the address `http://localhost:5000` and you will see the desktop as 
your background.

But, since Plash will read local static files for a web page, why not just give 
it the full path to your `public` folder? Well, that should work except for the 
way that the `index.html` file is setup. It is assuming that you are using a 
server and all addresses start with `/`. That will not load properly when Plash 
tries to load it as a static site.

To fix that, simply edit all the addresses to not have the `/` at the beginning. 
your `index.html` would then look like this:

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset='utf-8'>
	<meta name='viewport' content='width=device-width,initial-scale=1'>

	<title>Svelte app</title>

  <link rel='icon' type='image/png' href='favicon.png'>
  <link rel='stylesheet' href='global.css'>
  <link rel='stylesheet' href='build/bundle.css'>

<script defer src='build/bundle.js'></script>
</head>

<body>
</body>
</html>
```

This will load and run inside of Plash just fine without a webserver. It will 
also work fine for using a webserver as well. 

As you can see, Svelte takes all of our project files and compiles them into 
a single JavaScript file. There are no external libraries! Also, there are two 
CSS files: `global.css` and `bundle.css`. The `global.css` has anything that we 
setup as a global style using the `:global()` notation. The `bundle.css` has 
each style for each component instance. This insures that there are no name 
conflicts in styling from component to component.

## Conclusion

Now that you have the beginnings of your own desktop, start making your own 
widgets. You can send me a pull request to add them to the full package. I 
will be adding new widgets and eventually a local server in order to get 
hardware and file system items. Therefore, more tutorials to come...

