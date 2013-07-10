# blueimp Gallery

## Demo
[blueimp Gallery Demo](http://blueimp.github.io/Gallery/)

## Description
blueimp Gallery is a touch-enabled, responsive and customizable image and video gallery, carousel and lightbox, optimized for both mobile and desktop web browsers.  
It features swipe, mouse and keyboard navigation, transition effects, slideshow functionality, fullscreen support and on-demand content loading and can be extended to display additional content types.

## Setup
Copy the **css**, **img** and **js** directories to your website.

Include the Gallery stylesheet in the head section of your webpage:

```html
<link rel="stylesheet" href="css/blueimp-gallery.min.css">
```

Add the following HTML snippet with the Gallery widget to the body of your webpage:

```html
<!-- The Gallery as lightbox dialog, should be a child element of the document body -->
<div id="blueimp-gallery" class="blueimp-gallery">
    <div class="slides"></div>
    <h3 class="title"></h3>
    <a class="prev">‹</a>
    <a class="next">›</a>
    <a class="close">×</a>
    <a class="play-pause"></a>
    <ol class="indicator"></ol>
</div>
```

To initialize the Gallery with visible controls, add the CSS class **blueimp-gallery-controls** to the Gallery widget.

Include the Gallery script at the bottom of the body of your webpage:

```html
<script src="js/blueimp-gallery.min.js"></script>
```

Create a list of links to image files, optionally with enclosed thumbnails and add them to the body of your webpage, before including the Gallery script:

```html
<div id="links">
    <a href="images/banana.jpg" title="Banana">
        <img src="images/thumbnails/banana.jpg" alt="Banana">
    </a>
    <a href="images/apple.jpg" title="Apple">
        <img src="images/thumbnails/apple.jpg" alt="Apple">
    </a>
    <a href="images/orange.jpg" title="Orange">
        <img src="images/thumbnails/orange.jpg" alt="Orange">
    </a>
</div>
```

Add the following JavaScript code after including the Gallery script, to display the images in the Gallery lightbox on click of the links:

```html
<script>
document.getElementById('links').onclick = function (event) {
    event = event || window.event;
    var target = event.target || event.srcElement,
        link = target.src ? target.parentNode : target,
        options = {index: link},
        links = this.getElementsByTagName('a');
    if (blueimp.Gallery(links, options)) {
        return false;
    }
};
</script>
```

### Carousel setup
To display the images in an inline carousel instead of a lightbox, add the CSS class **blueimp-gallery-carousel** to the Gallery widget and remove the child element with the **close** class, or add a new Gallery widget with a different **id** to your webpage:

```html
<!-- The Gallery as inline carousel, can be positioned anywhere on the page -->
<div id="blueimp-gallery-carousel" class="blueimp-gallery blueimp-gallery-carousel">
    <div class="slides"></div>
    <h3 class="title"></h3>
    <a class="prev">‹</a>
    <a class="next">›</a>
    <a class="play-pause"></a>
    <ol class="indicator"></ol>
</div>
```

Add the following JavaScript code after including the Gallery script to initialize the carousel:

```html
<script>
blueimp.Gallery(
    document.getElementById('links').getElementsByTagName('a'),
    {
        container: '#blueimp-gallery-carousel',
        carousel: true
    }
);
</script>
```

## Options
The following are the default options set by the Gallery:

```js
var options = {
    // The Id, element or querySelector of the gallery widget:
    container: '#blueimp-gallery',
    // The tag name, Id, element or querySelector of the slides container:
    slidesContainer: 'div',
    // The tag name, Id, element or querySelector of the title element:
    titleElement: 'h3',
    // The tag name, Id, element or querySelector of the indicator container:
    indicatorContainer: 'ol',
    // The class to add when the gallery is visible:
    displayClass: 'blueimp-gallery-display',
    // The class to add when the gallery controls are visible:
    controlsClass: 'blueimp-gallery-controls',
    // The class to add when the gallery only displays one element:
    singleClass: 'blueimp-gallery-single',
    // The class to add when the left edge has been reached:
    leftEdgeClass: 'blueimp-gallery-left',
    // The class to add when the right edge has been reached:
    rightEdgeClass: 'blueimp-gallery-right',
    // The class to add when the automatic slideshow is active:
    playingClass: 'blueimp-gallery-playing',
    // The class for all slides:
    slideClass: 'slide',
    // The slide class for loading elements:
    slideLoadingClass: 'slide-loading',
    // The slide class for elements that failed to load:
    slideErrorClass: 'slide-error',
    // The class for the content element loaded into each slide:
    slideContentClass: 'slide-content',
    // The class for video content elements:
    videoContentClass: 'video-content',
    // The class for video when it is loading:
    videoLoadingClass: 'video-loading',
    // The class for video when it is playing:
    videoPlayingClass: 'video-playing',
    // The class for the "toggle" control:
    toggleClass: 'toggle',
    // The class for the "prev" control:
    prevClass: 'prev',
    // The class for the "next" control:
    nextClass: 'next',
    // The class for the "close" control:
    closeClass: 'close',
    // The class for the "play-pause" toggle control:
    playPauseClass: 'play-pause',
    // The class for the active indicator:
    activeClass: 'active',
    // The list object property (or data attribute) with the object type:
    typeProperty: 'type',
    // The list object property (or data attribute) with the object title:
    titleProperty: 'title',
    // The list object property (or data attribute) with the object URL:
    urlProperty: 'href',
    // The list object property (or data attribute) with the thumbnail URL,
    // used as alternative to a thumbnail child element:
    thumbnailProperty: 'thumbnail',
    // The list object property (or data attribute) for the video poster URL:
    videoPosterProperty: 'poster',
    // The list object property (or data attribute) for the video sources array:
    videoSourcesProperty: 'sources',
    // Defines if the gallery indicators should display a thumbnail:
    thumbnailIndicators: true,
    // Defines if the gallery slides are cleared from the gallery modal,
    // or reused for the next gallery initialization:
    clearSlides: true,
    // Defines if the gallery should open in fullscreen mode:
    fullScreen: false,
    // Defines if images should be stretched to fill the available space,
    // while maintaining their aspect ratio (will only be enabled for browsers
    // supporting background-size="contain", which excludes IE < 9):
    stretchImages: false,
    // Toggle the controls on pressing the Return key:
    toggleControlsOnReturn: true,
    // Toggle the automatic slideshow interval on pressing the Space key:
    toggleSlideshowOnSpace: true,
    // Navigate the gallery by pressing left and right on the keyboard:
    enableKeyboardNavigation: true,
    // Close the gallery on pressing the ESC key:
    closeOnEscape: true,
    // Close the gallery when clicking on an empty slide area:
    closeOnSlideClick: true,
    // Close the gallery by swiping up or down:
    closeOnSwipeUpOrDown: true,
    // Emulate touch events on mouse-pointer devices such as desktop browsers:
    emulateTouchEvents: true,
    // Hide the page scrollbars: 
    hidePageScrollbars: true,
    // Stops any touches on the container from scrolling the page:
    disableScroll: true,
    // Carousel mode (shortcut for carousel specific options):
    carousel: false,
    // Allow continuous navigation, moving from last to first
    // and from first to last slide:
    continuous: true,
    // Start with the automatic slideshow:
    startSlideshow: false,
    // Delay in milliseconds between slides for the automatic slideshow:
    slideshowInterval: 5000,
    // The starting index as integer.
    // Can also be an object of the given list,
    // or an equal object with the same url property:
    index: 0,
    // The number of elements to load around the current index:
    preloadRange: 2,
    // The transition speed between slide changes in milliseconds:
    transitionSpeed: 400,
    // The transition speed for automatic slide changes, set to an integer
    // greater 0 to override the default transition speed:
    slideshowTransitionSpeed: undefined,
    // Callback function executed on slide change.
    // Is called with the gallery instance as "this" object and the
    // current index and slide as arguments:
    onslide: undefined,
    // Callback function executed after the slide change transition.
    // Is called with the gallery instance as "this" object and the
    // current index and slide as arguments:
    onslideend: undefined,
    // Callback function executed on slide content load.
    // Is called with the gallery instance as "this" object and the
    // slide index and slide element as arguments:
    onslidecomplete: undefined,
    // Callback function executed when the Gallery is closed.
    // Is called with the gallery instance as "this" object:
    onclose: undefined
};
```

### Carousel options

If the **carousel** option is **true**, the following options are set to different default values:

```js
var carouselOptions = {
    hidePageScrollbars: false,
    toggleControlsOnReturn: false,
    toggleSlideshowOnSpace: false,
    enableKeyboardNavigation: false,
    closeOnEscape: false,
    closeOnSlideClick: false,
    closeOnSwipeUpOrDown: false,
    disableScroll: false,
    startSlideshow: true
};
```

The options object passed to the Gallery function extends the default options and also those options set via **carousel** mode.

### Container and element options
The widget **container** option can be set as id string (with "#" as prefix) or element node, so the following are equivalent:

```js
var options = {
    container: '#blueimp-gallery'
};
```

```js
var options = {
    container: document.getElementById('blueimp-gallery')
};
```

The **slidesContainer**, **titleElement** and **indicatorContainer** options can also be defined using a tag name, which selects the first tag of this kind found inside of the widget container:

```js
var options = {
    slidesContainer: 'div',
    titleElement: 'h3',
    indicatorContainer: 'ol'
};
```

It is also possible to define the container and element options with a more complex [querySelector](https://developer.mozilla.org/en-US/docs/Web/API/document.querySelector), although this won't work in IE7.

### Property options
The options ending with "Property" define how the properties of each link element are accessed.  
For example, the **urlProperty** is by default set to **href**. This allows to define link elements with **href** or **data-href** attributes:

```html
<div id="links">
    <a href="images/banana.jpg">Banana</a>
    <a data-href="images/apple.jpg">Apple</a>
</div>
```

If the links are passed as JavaScript array, it is also possible to define nested property names, by using the native JavaScript accessor syntax for the property string:

```js
blueimp.Gallery(
    [
        {
            data: {urls: ['http://example.org/images/banana.jpg']}
        },
        {
            data: {urls: ['http://example.org/images/apple.jpg']}
        }
    ],
    {
        urlProperty: 'data.urls[0]'
    }
);
```

## API
The blueimp Gallery can be initialized by simply calling it as a function with an array of links as first argument and an optional options object as second argument:

```js
var gallery = blueimp.Gallery(links, options);
```

The links array can be a list of URL strings or a list of objects with URL properties.  
The URL property name defined by each list object can be configured via the **urlProperty** option. By default, it is set to **href**, which allows to pass a list of HTML link elements as first argument.

The object returned by executing the Gallery function (the **gallery** variable in the example code above) is a new instance of the Gallery and allows to access the public API methods provided by the Gallery.  
The Gallery initialization function returns **false** if the given list was empty, the Gallery widget is missing, or the browser doesn't pass the functionality test.

### API methods

The Gallery object returned by executing the Gallery function provides the following public API methods:

```js
// Return the current slide index position:
var pos = gallery.getIndex();

// Return the total number of slides:
var count = gallery.getNumber();

// Move to the previous slide:
gallery.prev();

// Move to the next slide:
gallery.next();

// Move to the given slide index with the (optional) given duraction speed in milliseconds:
gallery.slide(index, duration);

// Start an automatic slideshow with the given delay (optional):
gallery.play(delay);

// Stop the automatic slideshow:
gallery.pause();

// Add additional slides after Gallery initialization:
gallery.add(list);

// Close and deinitialize the Gallery:
gallery.close();
```

### Videos
The Gallery can be initialized with a list of videos instead of images, or a combination of both:

```js
blueimp.Gallery([
    {
        title: 'Fruits',
        href: 'http://example.org/videos/fruits.mp4',
        type: 'video/mp4',
        poster: 'http://example.org/images/fruits.jpg'
    },
    {
        title: 'Banana',
        href: 'http://example.org/images/banana.jpg',
        type: 'image/jpeg',
        thumbnail: 'http://example.org/thumbnails/banana.jpg'
    }
]);
```

The Gallery uses the **type** property to determine the content type of the object to display.  
If the type property is empty or doesn't exist, the default type **image** is assumed.

For images, the **thumbnail** property defines the URL of the image thumbnail, which is used for the indicator navigation displayed at the bottom of the Gallery, if the controls are visible.

For videos, the **poster** property defines the URL of the poster image to display, before the video is started.

#### Multiple video sources
To provide multiple video formats, the **sources** property of a list object can be set to an array of objects with **href** and **type** properties for each video source. The first video format in the list that the browser can play will be displayed:

```js
blueimp.Gallery([
    {
        title: 'Fruits',
        type: 'video/*',
        poster: 'http://example.org/images/fruits.jpg',
        sources: [
            {
                href: 'http://example.org/videos/fruits.mp4',
                type: 'video/mp4'
            },
            {
                href: 'http://example.org/videos/fruits.ogg',
                type: 'video/ogg'
            }
        ]
    }
]);
```

It is also possible to define the video sources as data-attribute on a link element in [JSON](https://developer.mozilla.org/en-US/docs/JSON) array format:

```html
<div id="links">
    <a
        href="http://example.org/videos/fruits.mp4"
        title="Fruits"
        type="video/mp4"
        data-poster="http://example.org/images/fruits.jpg"
        data-sources='[{"href": "http://example.org/videos/fruits.mp4", "type": "video/mp4"}, {"href": "http://example.org/videos/fruits.ogg", "type": "video/ogg"}]'
    >Fruits</a>
</div>
```

### Additional content types
By extending the Gallery prototype with new factory methods, additional content types can be displayed.  By default, blueimp Gallery provides the **imageFactory** and **videoFactory** methods for **image** and **video** content types respectively.  

The Gallery uses the **type** property of each content object to determine which factory method to use.  The **type** defines the [Internet media type](http://en.wikipedia.org/wiki/Internet_media_type) of the content object and is composed of two or more parts: A type, a subtype, and zero or more optional parameters, e.g. **text/html; charset=UTF-8** for an HTML document with UTF-8 encoding.  
The main type (the string in front of the slash, **text** in the example above) is concatenated with the string **Factory** to create the factory method name, e.g. **textFactory**.

#### Example HTML text factory implementation
Although blueimp Gallery doesn't require [jQuery](http://jquery.com/), the following example uses it for convenience.

Extend the Gallery prototype with the **textFactory** method:

```js
blueimp.Gallery.prototype.textFactory = function (obj, callback) {
    var $element = $('<div>')
            .addClass('text-content')
            .attr('title', obj.title);
    $.get(obj.href)
        .done(function (result) {
            $element.html(result);
            callback({
                type: 'load',
                target: $element[0]
            });
        })
        .fail(function () {
            callback({
                type: 'error',
                target: $element[0]
            });
        });
    return $element[0];
};
```

Add the **text-content** class to the Gallery CSS:

```css
.blueimp-gallery > .slides > .slide > .text-content {
    overflow: auto;
    margin: 60px auto;
    padding: 0 60px;
    max-width: 920px;
    text-align: left;
}
```

With the previous changes in place, the Gallery can now handle HTML content types:

```js
blueimp.Gallery([
    {
        title: 'Noodle soup',
        href: 'http://example.org/text/noodle-soup.html',
        type: 'text/html'
    },
    {
        title: 'Tomato salad',
        href: 'http://example.org/text/tomato-salad.html',
        type: 'text/html'
    }
]);
```

## Requirements
blueimp Gallery doesn't require any other libraries and can be used standalone without any dependencies.

## Browsers
blueimp Gallery has been tested with and supports the following browsers:

### Desktop browsers

* Google Chrome 14.0+
* Apple Safari 4.0+
* Mozilla Firefox 4.0+
* Opera 10.0+
* Microsoft Internet Explorer 7.0+

### Mobile browsers

* Apple Safari on iOS 6.0+
* Google Chrome on iOS 6.0+
* Google Chrome on Android 4.0+
* Default Browser on Android 2.3+
* Opera Mobile 12.0+

## License
Released under the [MIT license](http://www.opensource.org/licenses/MIT).

## Credits
blueimp Gallery is based on [Swipe](http://swipejs.com/).
