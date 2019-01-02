# Problem
75% of the `wheel`/`mousewheel` event listeners that are registered on document level targets (window, window.document,
and window.document.body) do not specify any values for the `passive` option. Even though more than 98% of such listeners do
not call `preventDefault()` to prevent scrolling, the browser still needs to wait for the events to get handled before it
starts scrolling.
# Proposal
Our main goal is to reduce the delay between the time that the user starts scrolling by wheel\touchpad and the time that the 
display gets updated. We propose the wheel version of the [scroll intervention](https://developers.google.com/web/updates/2017/01/scrolling-intervention) 
which has been enabled in Chrome since 56 and later on in Firefox and Safari as well:  
Treat `wheel`/`mousewheel` event listeners that are added to document level targets (`window`, `window.document`, and 
`window.document.body`) as `passive` if they are not specified otherwise. For example code like:
```javascript
window.addEventListener("wheel", func);
```
will be equivalent to:
```javascript
window.addEventListener("wheel", func, {passive: true} );
```
For further details please check [touch](https://github.com/WICG/interventions/issues/35) and [wheel](https://github.com/WICG/interventions/issues/64) document level passive by default event listeners interventions in WICG.
