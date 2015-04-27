# Zoom to location from link outside of `<div id-'map'>` (Leaflet)

![](http://i1185.photobucket.com/albums/z344/buspainter2005/how-do/zoom1_zpswio2cuqw.gif)


## What's the deal?

Maybe you have a map and want to use hyperlinks text, buttons, pics, etc. that are outside of `<div id='map'></div>` to change where the map is centered and zoomed to. This seems to be a way to do, though I'm sure there are more efficient ways. 

[View full code on jsbin](http://jsbin.com/fupaho/4/)

Guidance from:

- [*Leaflet zoom onto location using link and map.setView*](http://stackoverflow.com/questions/25340051/leaflet-zoom-onto-location-using-link-and-map-setview), [Stack Overflow](http://stackoverflow.com/)
- [Response to *How to Get Element By Class in JavaScript?*](http://stackoverflow.com/a/3808837), [Stack Overflow](http://stackoverflow.com/)
- [document.querySelector](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector), [MDN](https://developer.mozilla.org/en-US/)

This requires we do a few things.

- a class to identify where the links will be &rarr; `map-navigation`
- links that contain location and zoom information information `<a href='' data-zoom='zoom level' data-position='lat, lon' >Link Text</a>`
- A way of accessing those links with location and zoom info &rarr; `document.querySelector()`

## HTML

- The parent `<div>` has `class='map-navigation'` applied to it
- We can then add our links &rarr; `<a href=''>Link Text</a>`.
	- Note that `href=''` is left empty so as not to add a URL hash (`#`). I'm sure there are cases when having a hash would be useful, but we'll leave it off for now
- Add the appropriate zoom level and location you want to map to go to with `data-zoom='zoom level'` and `data-position='lat, lon'`, respectively.

```html
<div class='map-navigation'>
	<div>
	<h3>Government Buildings</h3>
		<p><a href='' data-zoom='18' data-position='38.210133, -84.559359'>County Courthouse</a></p>
		<p><a href='' data-zoom='18' data-position='38.209501, -84.557031'>GSCPC</a></p>
	</div>
	<div>
	<h3>Schools</h3>
		<p><a href='' data-zoom='18' data-position='38.205853, -84.559008'>Garth</a></p>
		<p><a href='' data-zoom='18' data-position='38.207860, -84.554646'>Georgetown College</a></p>
		</p>
	</div>
</div>
```

## JavaScript

- `document.querySelector('.map-navigation').onclick = function(abc){...};`
	- Essentially we're asking this function to run when a thing is clicked within the `<div>` assigned `.map-navigation`
- `var pos = abc.target.getAttribute('data-position');`
	- Creates a variable `pos` that gets the `data-position` attribute of the element that was clicked
- `var zoom = abc.target.getAttribute('data-zoom');`
	- Creates a variable `zoom` that gets the `data-zoom` attribute of the element that was clicked
- `if (pos && zoom) {...]`
	- Checks to see if there is `pos` and `zoom` evaluate to `True`. In other words, do the `pos` and `zoom` variables both have a value? If yes, the code between `{...}` will run.
- `var locat = pos.split(',');`
	- Creates a local variable `locat` that takes the value of splitting the value of `pos` at the comma
- `var zoo = parseInt(zoom);`
	- Creates a local variable `zoo` that takes the value of turning `zoom` into an integer. `zoom` was a string, but Leaflet needs it to be an integer!
- `map.setView(locat, zoo, {animation: true});`
	- The values from `locat` and `zoo` are passed into Leaflet's `setView()` method.
	- `{animation: true}` activates a smoother transition from location to location
- `return false;`
	- Not sure why you do this

```JavaScript
document.querySelector('.map-navigation').onclick = function(abc) {
    var pos = abc.target.getAttribute('data-position');
    var zoom = abc.target.getAttribute('data-zoom');
    if (pos && zoom) {
        var locat = pos.split(',');
        var zoo = parseInt(zoom);
    map.setView(locat, zoo, {animation: true});
    return false;
    }
};
```