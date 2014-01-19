# Yet Another jQuery Carousel / Slider Thingy

It's better than all the others, of course:

* **Responsive** resizing on window resize (debounced, don't worry), height adapts to content
* **Swipe-enabled** for touch devices
* **Accessible** navigation elements (use your keyboard)
* **Circular mode** without cloning elements (they are shifted around instead)
* **Special features** like:
	* Adapt the height based on currently visible slides: [Example](http://backflip.github.io/jquery-carousel/demo/#example-06-b)
	* Add spacing between slides ("gutter"): [Example](http://backflip.github.io/jquery-carousel/demo/#example-06-d)
	* Have multiple visible slides with "grouped handles": [Example](http://backflip.github.io/jquery-carousel/demo/#example-06-a)
	* Sync multiple carousels: [Example](http://backflip.github.io/jquery-carousel/demo/#example-11-a)

Is uses Mark Dalgleish's [«Highly Configurable jQuery Plugins» pattern](http://markdalgleish.com/2011/05/creating-highly-configurable-jquery-plugins/).

**Tested on:** IE 7-10, iOS 7, current versions of Firefox, Chrome, Safari. It is highly likely to be working on older versions, too.

**Word of caution**: If you don't need the features listed above, this plugin might be overkill and something like [Swipe](https://github.com/bradbirdsall/Swipe) might serve you better.

## How to use

Demos: http://backflip.github.com/jquery-carousel/demo/

Basic markup (the node type doesn't matter, the elements are identified by class name):

```html
<div class="carousel" id="carousel">
	<div class="carousel-frame">
		<ul class="carousel-slider">
			<li class="carousel-slide">1</li>
			<li class="carousel-slide">2</li>
			<li class="carousel-slide">3</li>
		</ul>
	</div>

	<!-- Note: this is where navigational elements will be inserted if specified -->
</div>
```

* Include some basic styling (see [jquery.carousel.css](jquery.carousel.css))
* Include jQuery (>= 1.8) and the script
* Initialize carousel:
 
```js
$('#carousel').carousel(options);
``` 

or 

```js
var carousel = new Carousel($('#carousel'), options);
carousel.init();
```

## Methods

* **init(options)**: Add DOM elements and initialize carousel
* **enable**: Bind events for navigation, start autoplay if set
* **disable**: Unbind events for navigation stop autoplay
* **resize**: Resize elements based on available width and their content
* **goTo(index, skipAnimation)**
* **next**
* **prev**
* **update(options)**: Override current options and update carousel accordingly
* **destroy**: Remove added DOM elements, unbind events

## Default options

**Warning**: Some options were moved in version 1.2.

```js
{
	domSelectors: {
		frame: '.' + namespace + '-frame',
		slider: '.' + namespace + '-slider',
		slides: '.' + namespace + '-slide'
	},
	templates: {
		navContainer: '<div class="' + namespace + '-navs" aria-hidden="true" role="presentation" />',
		navItemPrev: '<button class="' + namespace + '-nav" role="presentation">Show previous slide</button>',
		navItemNext: '<button class="' + namespace + '-nav" role="presentation">Show next slide</button>',
		counter: '<div class="' + namespace + '-counter" aria-hidden="true" role="presentation">%current% of %total%</div>',
		handleContainer: '<div class="' + namespace + '-handles" aria-hidden="true" role="presentation" />',
		handleItem: '<button class="' + namespace + '-handle" role="presentation">Slide %index%</div>'
	},
	stateClasses: {
		isInitialized: 'is-initialized',
		isEnabled: 'is-enabled',
		isDisabled: 'is-disabled',
		isActive: 'is-active'
	},
	animation: {
		duration: 300, // milliseconds
		step: 1, // number of slides per animation (might be lower than number of visible slides)
		easing: 'ease-in-out'
	},
	behavior: {
		circular: false, // go to first slide after last one
		autoplay: 0, // auto-advance interval (0: no autoplay)
		pauseAutoplayOnHover: true,
		keyboardNav: true // enable arrow and [p][n] keys for prev / next actions
	},
	layout: {
		horizontal: true, // set to false for vertical slider
		groupedHandles: true, // combine handles to group if visibleSlides > 1 (e.g. "1-3", "4-6", "7")
		fixedHeight: true, // set height based on highest slide
		responsive: true, // whether to update the dimensions on window resize (debounced)
		visibleSlides: 1, // how many slides to fit within visible area (0: calculate based on initial width)
		gutter: 0 // spacing between slides
	},
	elements: { // which navigational elements to show
		prevNext: true, // buttons for previous / next slide
		handles: true, // button for each slide showing its index
		counter: true // "Slide x of y"
	},
	events: { // custom callbacks
		start: false, // function(targetDomIndex, targetSlideIndex) { … }
		stop: false // function(targetDomIndex, targetSlideIndex) { … }
	},
	initialSlide: 0, // which slide to show on init
	touch: { // whether to enable touch support and which criteria to use for swipe movement
		enabled: true,
		thresholds: {
			speed: 0.4, // multiplied by width of slider per second
			distance: 0.3 // multiplied by width of slider
		}
	},
	$syncedCarousels: null // jQuery collection of carousel elements to sync with
}
```
