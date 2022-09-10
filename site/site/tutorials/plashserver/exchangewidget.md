---
date: 2020-03-02
title: Creating the Exchange Rate Widget
---

# {{title}}

#### {{cdate date 'MMMM D, YYYY'}}

Since I'm an American living in Thailand, I like to keep up with current exchange
rates. It's really nice to have it on my background so that I can see it easily. So, 
why not add it to the PlashServer! Here we go....

## `Exchange.svelte` file

In the `UI/src/components` directory, create the file `Exchange.svelte` and start 
adding the following code. I'll show the code in sections and describe what I'm 
doing. 

This component gets information from the internet to display on the background. 
Therefore, I'm using the `{#await...}...{/await}` directive to get and display the information 
from a promise.

As always, I like to start with the component template:

```html
<div id='Exchange' style="top: {top}px; 
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
    {:then amount}
      1 {config.from} is {amount} {config.to}
    {:catch e}
      1 {config.from} is {savedAmount} {config.to}
    {/await}
  </p>
</div>
```
This template starts with the `div` that positions the widget in the background 
using absolute placement. The next element is the `p` element for styling the 
words used to describe the current exchange rate. I'm a programmer that
isn't best at making styles. If anyone wants to give styling suggestions, 
I would really love it.

Inside the `p` tag, You see the `{#await ...}....{/await}` structure. This is 
the workhorse for promises in Svelte. The `load` varaible is the variable that 
contains the promise that the template is waiting for resolution. Between the 
`{#await load}` and the `{:then amount}` is what will be displayed while waiting 
on the promise to be fulfilled. Here, I have `Loading...`, but you can insert 
anything you want.

When the promise is fulfilled, the area between the `{:then amount}` and the 
`{:catch e}` will be displayed. The `amount` variable is the data returned by 
the promise. It isn't a variable that is already declared in your JavaScript 
section, but a new variable and should be named accordingly. That new variable 
is then used in the template to display the information retrieved from the website.

If there is a problem retrieving the information (site not available, network 
issues, etc), then the section between the `{:catch e}` and the `{/await}` will 
be displayed. The `e` variable will contain information about the error. But, I'm 
not interested in that. I want to show the last successful calculation. Therefore, 
I'm displaying the variable `savedAmount` that is used to store the last calculated 
exchange rate. As you can see, you don't have to make use of the `e` variable, but 
you do have to declare it.

```html

<style>
  #Exchange {
    position: absolute;
    font-weight: bold;
  }
</style>

```

The style section simply declares the way the widget is to be positioned on 
the screen (absolutely) and the font weight to use. 

```javascript
<script>
  import { onMount } from 'svelte';
  import { thirtyMinute } from '../store/thirtyMinuteStore.js';

  export let top;
  export let left;
  export let style;
  export let config;
  let load;
  let savedAmount;
```

The code section starts as normal. I'm importing the `onMount` function to execute 
instruction upon mounting the widget. I'm also getting the `thirtyMinute` store to 
get updates every thirty minutes to reload the exchange rate. In reality, the 
exchange rate changes at most once an hour. I'm using the thirty minute timer in 
order to not have another timer running. Each timer in the background uses resources. 
I feel it's best to minimize the number of different timers.

The export section has the normal parameters for all widgets. The only new variables 
are the `load` variable to contain the promise, and the `savedAmount` variable to 
contain the last successfully download exchange rate.

```javascript
  onMount(() => {
    var unsubscribeThirtyMinute = thirtyMinute.subscribe((value) => {
      getExchangeRate();
    });

    getExchangeRate();
    
    return(() => {
      unsubscribeThirtyMinute();
    });
  });
```

The `onMount` function does the subscription to the `thirtyMinute` store that 
is updated every thirty minutes. We ignore the value since it doesn't matter for
this application. But, we could easily only call the `getExchangeRate()` function 
for even values of `value`. That would then update once an hour.

Currently, every time the store is updated, the `getExchangeRate()` function is called. 
It is also called after the subscription in order to get an initial value. The return 
gives Svelte the function to unsubscribe to the store when the widget is unloaded from 
the DOM.

```javascript
  function getExchangeRate() {
    //
    // Get the current exchange rate.
    //
    load = fetch('https://api.exchangeratesapi.io/latest?symbols=' + config.from + ',' + config.to)
    .then((response) => {
      return response.json();
    })
    .then((data) => {
      savedAmount = round_to_precision(data.rates[config.to]/data.rates[config.from], 0.05);
      return(savedAmount);
    });
  }
  
  function round_to_precision(x, precision) {
    var y = +x + (precision === undefined ? 0.5 : precision/2);
    return y - (y % (precision === undefined ? 1 : +precision));
  }
</script>
```

The last two functions are `getExchangeRate()` which does all the work for this 
widget and `round_to_precision()` which creates the proper precision for the 
exchange rate. I'm getting the exchage rate information from a free API: https://api.exchangeratesapi.io.
This API has a funny way it works: it gives the `from` exchange rate not as a whole 
number. To get the proper exchange rate for one unit of the `from` currency, you 
have to divide the `to` currency by the `from` currency. Not sure for the reason for this, 
but it does work. 

The `getExchangeRate()` uses the `fetch API` to get the information from the server. 
Since it comes as a JSON structure, the first `.then()` clause is used to convert the 
response to JSON. Whatever is returned from that clause will go to the next `.then()` 
clause that will then calculate the exchange rate and put it into the `savedAmount` 
variable. Since this variable is only updated upon a successful retrieval from the 
API, it stores each successful attempt. This value is then returned which is then 
placed in the `amount` variable in the template. Since the exception catching is 
done in the template, I don't need to have a `.catch()` attached to the promise chain.

## Adding the New Widget

In the `src/main.js` file, we need to add the information to add the new Exchange rate 
widget. Therefore, open that file in your editor and start adding the following. At the 
top, we need to load in the new widget:

```javascript
import Exchange from './components/Exchange.svelte';
```

Then we need to add the config information to the `widgets` structure. So, just before 
the `Time` widget, add this:

```javascript
  {
    name: 'Exchange',
    widget: Exchange,
    top: 220,
    left: 35,
    style: {
      font: 'Alfa Slab One',
      size: 30,
      color: 'lightblue'
    },
    config: {
      from: 'USD',
      to: 'THB',
      shadow: '1px 1px 0px black, 2px 2px 0px black, 3px 3px 0px black, 4px 4px 0px black, 5px 5px 0px black, 6px 6px 2px black'
    }
  },
```

In the `config` section of the `Exchange` widget, you can set the currency your interested in seeing. 
The `from` should be the currency you want to use as the basis. Here, I'm using the `USD` for the 
United States Dollar. The `to` contains `THB` for the Thai Baht, which is the
currency used in Thailand. You can get the complete list of supported currency
names from their website.

I adjusted the top position to place it just under the `Time` widget. I also
change the color so it looks different from the `Time` widget. 

## Conclusion

After you compile and reload, you should have the currency you selected
displayed in your background. Now that you know how to use the
`{#await}...{/await}` structures, go and create more widgets that get their
information from the internet. The only limits are your imagination.

Since summer is starting here in Thailand with raining season next, I better
work on a weather widget for my desktop. Keep watching for the next widget
installation!
