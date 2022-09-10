---
date: 2020-03-20
title: Creating the Covid-19 Widget
---

# {{title}}

#### {{cdate date 'MMMM D, YYYY'}}

Okay, I know I said I would be working on a weather widget, but
the current problems with [Covid-19](https://www.who.int/emergencies/diseases/novel-coronavirus-2019)
has caused me to create a small widget to show the number of active 
infections and deaths. The widget will display the information for 
any country you set for it. On my background, I'm showing Thailand (where I live) and 
the USA (where I'm from).

### Corvid19.svelte File

In the `src/components` directory, create the file `Corvid19.svelte` and put the following: 

```html
<div id='Corvid19' style="top: {top}px; 
                      left: {left}px;" 
>
  <p
    style="text-shadow: {config.shadow};
           font-family: '{style.font}'; 
           font-size: {style.size}px; 
           color: {style.color};"
  >
    {#await load}
      Loading...
    {:then data}
      {typeof data === 'undefined' ? corData.country : data.country} - Active: {typeof data === 'undefined' ?  corData.active : data.active} , Died: {typeof data === 'undefined' ?  corData.deaths : data.deaths}
    {:catch e}
      {corData.country} - Active: {corData.active} , Died: {corData.deaths}

    {/await}
  </p>
</div>

<style>
  #Corvid19 {
    position: absolute;
    font-weight: bold;
  }
</style>

<script>
  import { onMount } from 'svelte';
  import { thirtyMinute } from '../store/thirtyMinuteStore.js';

  export let top;
  export let left;
  export let style;
  export let config;
  
  let load;
  let corData = {
    country: 'loading',
    cases: 'loading',
    active: 'loading',
    deaths: 'loading',
    todayCases: 'loading',
    todayDeaths: 'loading',
    recovered: 'loading',
    critical: 'loading',
    casesPerOneMillion: 'loading'
  };
  
  onMount(() => {
    var unsubscribeThirtyMinute = thirtyMinute.subscribe((value) => {
      getInfectionRate();
    });
    getInfectionRate();
    return(() => {
      unsubscribeThirtyMinute();
    });
  });

  function getInfectionRate() {
    //
    // Get the current information about Corvid-19 has this struture:
    //
    //country	"Thailand"
    //cases	212
    //todayCases	0
    //deaths	1
    //todayDeaths	0
    //recovered	42
    //active	169
    //critical	1
    //casesPerOneMillion	3
    //
    load = fetch('https://corona.lmao.ninja/v2/countries/' + config.country)
    .then((response) => {
      return response.json();
    })
    .then((data) => {
      corData = data;
      return(data);
    });
  }
</script>
```

If you say this is just like the `Exchange.svelte` file, you would be right. I copied 
that one to create this one. Once you start making many widgets, you can copy one that 
is similar to the one you want to make and you have a great template to start from.

The biggest change is in the template and the function that retrieves the information. 
The template is showing more information than the last one. Also, since this site is 
very slow, the template will get rendered every now and then with a null for the `data` 
in the `{#await...}...{/await}` conditional. Therefore, we have to check the data 
and make sure it's okay.

The function `getInfectionRate()` retrieves the information from the public API `https://corona.lmao.ninja`.
This api is very easy to use as you can see from the code. 

### Text.svelte File

The next widget is a very simple text widget. You can use it to place text anywhere 
on your desktop. Create the file `src/components/Text.svelte` and put this into it:

```html
<div id='Text' style="top: {top}px; 
                      left: {left}px;" 
>
  <p
    style="text-shadow: {config.shadow};
           font-family: '{style.font}'; 
           font-size: {style.size}px; 
           color: {style.color};"
  >
    {config.text}
  </p>
</div>

<style>
  #Text {
    position: absolute;
    font-weight: bold;
  }
</style>

<script>
  export let top;
  export let left;
  export let style;
  export let config;
</script>
```

The text in the variable `config.text` is put inside of the paragraph tag with 
formatting for it. I'm using this to title the listing of the two countries that 
I want to see the information about.

### Adding to the `main.js`

Now, all you need to do is add the new widgets to the `main.js` file and setup 
their configuration. I'm not going to show everything in that file (it's starting 
to get very large). Just the new stuff will be shown.

```JavaScript
import Corvid19 from './components/Corvid19.svelte';
import Text from './components/Text.svelte';
```

In the inport section at the top, add these lines to import the two new 
widgets.

```JavaScript
const widgets = [{
  name: 'Corvd19Text',
  widget: Text,
  top: 300,
  left: 100,
  style: {
    font: 'Alfa Slab One',
    size: 30,
    color: 'lightblue'
  },
  config: {
    text: 'Corvid-19 Cases',
    shadow: '1px 1px 0px black, 2px 2px 0px black, 3px 3px 0px black, 4px 4px 0px black, 5px 5px 0px black, 6px 6px 2px black'
  }},{
  name: 'Corvid19-US',
  widget: Corvid19,
  top: 380,
  left: 35,
  style: {
    font: 'Alfa Slab One',
    size: 30,
    color: 'lightblue'
  },
  config: {
    country: 'usa',
    shadow: '1px 1px 0px black, 2px 2px 0px black, 3px 3px 0px black, 4px 4px 0px black, 5px 5px 0px black, 6px 6px 2px black'
  }},{
  name: 'Corvid19-Thailand',
  widget: Corvid19,
  top: 340,
  left: 35,
  style: {
    font: 'Alfa Slab One',
    size: 30,
    color: 'lightblue'
  },
  config: {
    country: 'thailand',
    shadow: '1px 1px 0px black, 2px 2px 0px black, 3px 3px 0px black, 4px 4px 0px black, 5px 5px 0px black, 6px 6px 2px black'
  }},
```

Next, I'm adding the `Corvid19` widget twice with their proper configurations and 
the `Text` widget once. I'm making sure to give every widget a unique name. You 
can change these as you like. This configuration gives this result:

![Corvid19 and Text Widgets Added](/imgs/corvid19.png)

Remember, is isn't the full file. It is just the parts I changed to add these new 
widgets. If your uncertain on what it is [check out](https://github.com/raguay/SveltePlashServer) 
the repository to get the full view.

### Conclusion

Now you can track what Corvid-19 is doing in your country. But, remember, this 
isn't for creating fear, but for getting information to make right choices!

