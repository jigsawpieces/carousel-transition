# Carousel transition effects

This is a short tutorial on how to add in transition effects for the carousel slider.

Our basic carousel markup is structured like this:

```html
<section class="carousel">
	
	<ul class="carouselSlides">
	
		<li class="carouselSlide"></li>
        <li class="carouselSlide hidden"></li>
        <li class="carouselSlide hidden"></li>
	
	</ul>

</section>
```

The **.hidden** class is added to slides which we want to hide. When we click on either the carousel controls or carousel button, jQuery is used to add/remove this class the relevant slides. The default CSS values for the **.hidden** class are as follows:

```css
.hidden {
    display: none !important;
    visibility: hidden;
}
```

Simply adding CSS transitions to the list item won't work, because CSS transitions doesn't effect the display property (see full answer here: http://stackoverflow.com/a/22103238). Therefore, instead of using **display: block** and **display: none** to hide/show the slides, we need to use **opacity: 1** and **opacity: 0**

Firstly, we need to overwrite the **.hidden** class so that the element is always displayed, but set to **opacity: 0** when we don't want it to be shown:
```css
.carousel ul.carouselSlides li.carouselSlide.hidden {
    display: block !important;
    opacity: 0;
}
```

Then we need to add the default opacity and transition properties to the carousel slides itself:

```css
.carousel ul.carouselSlides li.carouselSlide  {
    display: block;
    opacity: 1;
    transition: opacity 1s ease-in-out;
}
```

We also need to explicitly define the value of the parent container as well to create the "viewer", and stack the slides on top of each other so that they can fade from one to the other.

```css
.carousel ul.carouselSlides {
    overflow: hidden;
	position: relative; /** set position to relative **/
	height: 450px; /** define the height of the parent **/
}

.carousel ul.carouselSlides li.carouselSlide{
    display: block;
    opacity: 1;
    transition: opacity 1s ease-in-out;
    position: absolute; /** position the slides absolutely relative to the parent **/
    left: 0;
    top: 0;
    width: 100%;
}
```

Lastly, don't forget to un-hide the carousel controls!

```css
.carousel .carouselControls {
    display: block;
}

```

### Files

- See the CSS folder for an example of the working CSS files

### Notes

- This fix will only work for browsers that support the CSS3 transitions property. For browsers that don't support CSS3 transitions, the slider will still work but without the transition effect. For full list of browser support see: http://caniuse.com/#feat=css-transitions
- The parent container must have an explict height defined, and overflow set to hidden. 
- Slide list items must be absolutely positioned in order to create the fade in/out effect.



