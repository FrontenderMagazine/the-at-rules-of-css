The `at-rule` is a statement that provides CSS with instructions to perform or
how to behave. Each statement begins with an`@` followed directly by one of
several available keywords that acts as the identifier for what CSS should do. 
This is the common syntax, though each`at-rule` is a variation of it.

### Regular Rules

Regular rules are ones that follow a regular syntax:

    @[KEYWORD] (RULE);

#### `@charset`

This rule defines the character set used by the browser. It comes in handy if
the stylesheet contains non
-[ASCII characters][1] (e.g. [UTF-8][2]). Note that a character set that is 
[placed on the HTTP header][3] will override any `@charset` rule.

    @charset "UTF-8";

#### `@import`

This rule instructs the stylesheet to request and include an external CSS file
as if the contents of that file were right where that line is.

    @import 'global.css';

With the popularity of CSS prepreprocessors that support @import, it should be
noted that they work differently than native CSS does. Preprocessors will fetch 
that file and process them together into a single CSS file. In native CSS, each
@import is a separate HTTP request for that file.

#### `@namespace`

This rule is particularly useful for applying CSS to XML HTML (XHTML) so that
XHTML elements can be used as selectors in the CSS.

    /* Namespace for XHTML */
    @namespace url(http://www.w3.org/1999/xhtml);
    
    /* Namespace for SVG embedded in XHTML */
    @namespace svg url(http://www.w3.org/2000/svg);

### Nested Rules

Nested rules contain a subset of additional statements, some of which might be
conditional to a specific situation.

    @[KEYWORD] {
      /* Nested Statements */
    }

#### `@document`

This rule specifies conditions for styles that apply to a specific page. For
example, we can provide a URL then customize the styles for that particular page.
Those styles will be ignored on other pages.

    @document 
      /* Rules for a specific page */
      url(http://css-tricks.com/),
      
      /* Rules for pages with a URL that begin with... */
      url-prefix(http://css-tricks.com/snippets/),
      
      /* Rules for any page hosted on a domain */
      domain(css-tricks.com),
    
      /* Rules for all secure pages */
      regexp("https:.*")
    {
      
      /* Start styling */
      body { font-family: Comic Sans; }
    
    }

The support for `@document` is pretty weak at the time of this writing:

| Chrome | Safari | Firefox | Opera | IE | Android | iOS |

| No     | No     | -
moz    | No    | No | No      | No
|

#### `@font-face`

This rule allows us to load custom fonts on a webpage. There are 
[varying levels of support][4] for custom fonts, but this rule accepts
statements that create and serve those fonts.

    @font-face {
      font-family: 'MyWebFont';
      src:  url('myfont.woff2') format('woff2'),
            url('myfont.woff') format('woff');
    }

#### `@keyframes`

This rule is the basis for [keyframe][5] [animations][6] on many CSS properties
, by allowing us to mark the start and stop (and in-between) marks for what is 
being animated.

    @keyframes pulse {
      0% {
        background-color: #001f3f;
      }
      100% {
        background-color: #ff4136;
      }
    }

#### `@media`

This rule contains conditional statements for targeting styles to specific
screens. These statements can include screen sizes, which can be useful for
[adapting styles to devices][7]:

    /* iPhone in Portrait and Landscape */
    @media only screen 
      and (min-device-width: 320px) 
      and (max-device-width: 480px)
      and (-webkit-min-device-pixel-ratio: 2) {
    
        .module { width: 100%; }
    
    }

Or applying styles only to the document when it is printed:

    @media print {
    
    }

#### `@page`

This rule defines styles that are to individual pages when printing the
document. It specifically contains pseudo-elements for styling the`:first` page
as well as the`:left` and `:right` margins of the page.

    @page :first {
      margin: 1in;
    }

#### `@supports`

This rule tests whether a browser supports a feature, then applies the styles
for those elements if the condition is met. It's sort of like[Modernizr][8] but
tailored specially for CSS properties.

    /* Check one supported condition */
    @supports (display: flex) {
      .module { display: flex; }
    }
    
    /* Check multiple conditions */
    @supports (display: flex) and (-webkit-appearance: checkbox) {
      .module { display: flex; }
    }

Here's the, uh, support for @supports:

| Chrome | Safari | Firefox | Opera | IE   | Android | iOS |

| 28+    | No
| 31+     | 12.1+ | Edge | 4.4+    | No
|

### Wrapping Up

The `at-rule` is where it's at for making CSS do some crazy and interesting
things. While the examples here are basic, we can see how they might be used to 
handcraft styles to very specific conditions, thereby creating user experiences 
and interactions that match a scenario.

[Twitter][9] [Facebook][10] [Google+][11]

 [1]: http://www.ascii.cl/htmlcodes.htm
 [2]: http://en.wikipedia.org/wiki/UTF-8
 [3]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta#Attributes
 [4]: https://css-tricks.com/snippets/css/using-font-face/
 [5]: https://css-tricks.com/snippets/css/keyframe-animation-syntax/
 [6]: https://css-tricks.com/almanac/properties/a/animation/
 [7]: https://css-tricks.com/snippets/css/media-queries-for-standard-devices/
 [8]: http://modernizr.com/

 [9]: https://twitter.com/intent/tweet?text=The%20At-Rules%20of%20CSS&url=https://css-tricks.com/the-at-rules-of-css/&via=real_css_tricks

 [10]: https://www.facebook.com/sharer/sharer.php?u=https://css-tricks.com/the-at-rules-of-css/

 [11]: https://plus.google.com/share?url=https://css-tricks.com/the-at-rules-of-css/