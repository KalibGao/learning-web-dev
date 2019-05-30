# HTML

<meta name="viewport" content="width=device-width, initial-scale=1">

This is the responsive meta tag. It tells the browser to set the content width to the viewport one, ensuring
for the content to adapt automatically. It also tells the browser to set the zoom level to 1 initially, while still
allowing the user to zoom in (especially on mobile phones).

Before writing any CSS, you have to start with the most important of a webpage: the **content**.

# Base CSS

**BEST PRACTICE** 
*Order your CSS rules alphabetically*
When editing a CSS file, finding the declaration to change can be time consuming.
To reduce the cognitive load when both reading and writing rules, write them alphabetically.
It's the only sorting rule that is future-proof because it's opinionless.
When you will have more than 10 CSS declarations in a rule, you will be glad to know where to find what you
were looking for in a split second!

The `line-height` has a unitless value of 1.5 . It means each line of text will be 1.5 times the element's current font size. For most of the page, and combined with the `font-size: 16px` declaration, this will make each line of text 24px high.

I always have a `min-width: 300px` that prevents the page from being too narrow to be readable.

The `min-height: 100vh` ensures the page to be at least as tall as 100% of the viewport height ( vh ).

The `overflow-x: hidden` declaration prevents the page from scrolling horizontally while preserving the
usual vertical scroll.

### Links

Using `currentColor` is prefered because it will pick up the color set by html before: color: #fff .
Updating the color of both only requires a single line change.

Sometimes, the hand cursor doesn't show up when hovering a link. That's why I always add `cursor: pointer` to force the hand to show up.

# Layout

Background image with no <img> tag:
This image is not displayed with an <img> tag because its purpose is decorative and belongs in the CSS.

**BEST PRACTICE** 
*Avoid the shorthand notation*
We're using each background-* property instead of the shorthand background one.
If you use `background: red` , you are essentially setting `background-color: red` and *reseting all other properties to their initial value*. [(aconteceu comigo uma vez definindo o "border")]
It becomes a problem when you actually override a declaration you had previously written, and you wonder why your CSS line doesn't work!
If `background-color` had been set earlier, it would have been undone here. The only useful shorthand properties are margin , padding and border.

We enable Flexbox on the .content by simply using `display: flex`. This makes both .side and
.about Flexbox items.

The `position: relative` allows .content to appear above .wallpaper , and the `min-height` is
here to make sure .content covers the whole page.

The use of `max-width` is very practical: it just means that at any point we don't want an element to by
wider than a certain value. For readability reasons we want the .about section to never go beyond
26rem in width (which is 26 x 16px = 676px ). Since it's a block element, it will use the whole width
available up to a certain point. Depending on the length of your written content, you can play with the value
here.

**BEST PRACTICE**
*Avoid z-index when possible*
All positioned elements ( absolute , fixed , or relative ) can have a z-index value to stack them relatively to each other.
But elements are already stacked based on their location within the HTML code.
Because .wallpaper and .content are siblings, the second one .content will appear above (only if it's positioned too).
And child elements will appear above their parent.
It's better to place them as you want in your HTML, otherwise you'll have to keep track of all z-index values
throughout your CSS.


Desktop view -- On desktop, we want the layout to be horizontal instead.

The `.content` uses the default value of `flex-direction` which is row , meaning the items ( .side and .about ) are spread out horizontally. _`justify-content` appears twice because the `space-evenly` value is not available in all browsers, so we use `space-around` as a reasonable fallback_.

The .side element (which contains the image), has fixed dimensions of a 20rem by 20rem square. _If there's more horizontal space available, we don't want it to grow, hence the `flex-grow: 0`_. On the other hand, we also don't want it to shrink at all, otherwise, the image would be squased. That's why flex-shrink: 0 is used here too. We basically want the .side to be 20rem by 20rem at all times. 

We also want it to appear after the text content, which is why we use order: 2 . For the .about , we do want it to use the remaining space available, in both directions, which is why `flex-grow` and `flex-shrink` have both a value of 1 .

**BEST PRACTICE**
_In media queries, don’t undo, just do_
With mobile-first approaches, it's easy to make a layout work well on narrow screens, and then "undo" most of it on desktop. But that's tricky because you have to keep track of what has been done outside of media queries, and reset those values inside the desktop media query. You also end up writing a lot of CSS just to reset values, and you can end up leaving CSS like margin-bottom: 0 you are not sure what.
The margin-bottom set for the .side element should only appear on mobile.
Instead of applying a margin by default on all screens, and removing it on desktop, we only apply it on mobile.

# Styling the elements

### The picture

The shadow is separated from the image because we are going to animate them separately later on.

The `padding-top: 100%` is a technique that makes the .picture as high as it is wide making it square
at all times. It also has a position: relative so that it acts as a reference point for its two absolutely
positioned children.

The `border-radius` is set to the very high value of 290486px to ensure the elements to be rounded. You
can use any extremely high value. I personaly use 290486px as a trademark because it's my date of birth.

### The name

The name is the most important information of the page. That's why it uses the <h1> HTML tag, which has the strongest semantic value. To reflect this prominence visually as well, we are gonna make it bigger.

The font size uses the rem unit: it's the root value, equal to the font size set on the html element, which we previously set to 16px . So 2.25rem is essentially 36px . Using rem is useful because it references a common value, and we can update the html value to set all instances of rem values.

The line-height is set to 1.125 It's hard to see its purpose if the text is too short (resize your browser to reach two lines), but keeping the page value of 1.5 makes the two lines too spaced out.

**BEST PRACTICE**
_Set line-height first, margin/padding second_
Some developers use the line-height as a way to give space to an element. But as its name suggests, it's meant to define the height of a single line, not the space between each line.
The line-height value should be set for readability purposes only.
If you need to give more breathing space to an element, just use a bit of margin (or sometimes padding), which is what we're doing here with margin-bottom .

The hr line

The horizontal rule ( `hr` ) defines a semantic break between blocks of text. While keeping this semantic value intact, we want to make this line more subtle.

For more control, we're removing the border and using the background-color with a height of 1px to define a thin short line.

The `transform-origin` will be used when we animate the width later on.

By using `display: inline-block` we combine two behaviors:

* inline makes sure the width is equal to its content (the button) 
* block makes sure surrounding elements will appear above and below 
* it also allows us to use margin-top.

The `em` unit is equal to the current font size. In this case, it's similar to the unitless line height value.
The font size uses the `rem` unit: it's the root value, equal to the font size set on the html element.

The button uses the same inline-block technique as its parent.

The height of the button is proportional to the font size, and equal to 3.5 times the font size value:
* the unitless line-height is equal to 1 or 0.875rem
* the vertical paddings (top and bottom) are set to 1.25em each, or 1.25 times the font size

The em unit is equal to the current font size. In this case, it's similar to the unitless line height value.

If you play around with the font-size value, by setting 2rem for example, you'll notice that the button will resize proportionally. This is very useful because we only need to update a single value to increase/decrease the size of the button, while maintaining a perfect ratio.

We also apply some other styles:
* because of the colored background and the darker text color, we remove the text-shadow
* we use `user-select: none` so the text content can't be selected, which can happen when clicking repeatedly on the button
* to make sure the text never is displayed on two lines, we use `white-space: nowrap`

### Button states

The button is the main interaction element of the page. Visitors can hover the button and click on it.

The `transition-property` and `will-change` values are for the button states.

The box shadow is transparent so it can work on any background color. For the transformation, we increase the button's size by 2% with `scale(1.02)` and move it upwards by a few pixels with `translateY(-4px)` .

When clicking the button, we want to make it look as if it was pressed downward.

We're just playing with the same properties but with different values. The shadow is stronger and smaller because the button appears closer to the "ground".

Play with the transition-duration value set in the 2. Shared section to see it slower or faster.

# Font-Awesome

We are including the whole Font Awesome library directly from the CDN. The benefit is that all icons are available. The disadvantage is that the files loaded are much bigger in size. You can use an icon font generator like _IcoMoon_ or _Fontello_ to only include the icons you actually need. This will reduce the size of the font files. One other option is to use SVG images directly, but that's trickier!

<script defer src="https://use.fontawesome.com/releases/v5.0.0/js/all.js"></script>

**Interessante**
If you reload the page repeatedly, you might notice that the layout "jumps" for a split second. That's because at first, the icons are not loaded, and the page only displays the text and the images. Then, when the icons finally load, the pop up, and cause the page to be redrawn, hence the jump.

To avoid this jump, we're gonna set a square area of 2rem by 2rem for each <li> list item.

# CSS Animations

Animating in CSS is basically changing a set of values over time. For example, fading in an element is done by setting the `opacity` to zero `0` , and gradually incrementing it ( 0.1 , 0.2 , 0.3 …) until you finally reach the value of `1`.

It would take a while to figure all the intermediate values. Luckily in CSS, you only need to set 2 values:

* the start values, with the keyword `from`
* the end values, with the keyword `to`

Everything in between will be determined by:

* the `animation-duration` : how long it takes to go from the start to the end
* the `animation-timing-function` : how the values in between are calculated (based on a curve)

CSS Animations are triggered when the page loads, or when a class name changes.
