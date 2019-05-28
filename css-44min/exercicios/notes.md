<meta name="viewport" content="width=device-width, initial-scale=1">

This is the responsive meta tag. It tells the browser to set the content width to the viewport one, ensuring
for the content to adapt automatically. It also tells the browser to set the zoom level to 1 initially, while still
allowing the user to zoom in (especially on mobile phones).

Before writing any CSS, you have to start with the most important of a webpage: the **content**.

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

## Links

Using `currentColor` is prefered because it will pick up the color set by html before: color: #fff .
Updating the color of both only requires a single line change.

Sometimes, the hand cursor doesn't show up when hovering a link. That's why I always add `cursor: pointer` to force the hand to show up.

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