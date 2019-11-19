---
date: 2019-11-19
title: Updated Svelte Site and Template
---
 
# {{title}}
 
#### {{cdate date 'MMMM D, YYYY'}}
 
I just did a major update to this site and my [Svelte GitHub Site Template](https://github.com/raguay/SvelteGithubSiteTemplate).
This change fixed the problems with not loading the partials before trying to display a page that has
partials. Also, since GitHub always gives a `200` response on getting a raw page that doesn't exist (It just sends 
the front page for the GitHub pages account), I had to detect that in order to show the error page. I also never 
unsubscribed from stores when a component was removed. After a while, changing pages would get slower and slower. I've
now have fixed that as well.

The styling for the site has been moved to the info store. Now, to change the colors and text sizes, go to the 
info store and make the changes. This also means that styling can now be programmically changed (remove the sidebar, 
show the sidebar on the left or right, etc.). This gives the framework much more flexibility.

I also just updated the [Favorite Tools](/#/favtools) page to list frameworks as well. Of course, I listed [Svelte](https://svelte.dev/) 
as my main framework to use! If you haven't tried it yet, you should. 

I have many more ideas to add to this framework. Stay tuned for more developments!

