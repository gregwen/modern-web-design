### Lesson 4: Getting Started with CSS

[TOC]

#### Chapter 1: CSS Structures and Nomenclature

- Cascading Stylesheets contain one or more **rulesets**.

    - ```css
        p{
            color: red;
        }
        
        ul, ol {
            color: green;
        }
        
        li{
            font-size: 2em;
        }
        ```

    - A rule set has two parts: A `selector` and a `declaration`.

    - The selector comes before the curly braces `{ },` and the declaration lies inside the braces.

        - A selector can propose more than one match, called a **compound** selector.

            ```css
            p, ol, ul, dl, figure {
                color: red;
            }
            ```

        - A declaration block (`color: red;`) contains one or more declarations

            ```css
            p{
                color: red;
                font-weight: bold;
            }
            ```

        - Separate the declarations with semicolons.

        - A declaration has two parts: A **property** `color` and a **value** of `red`.

    - Style rules should be kept in a style sheet, not inline.

    - You can use linked stylesheets or embedded stylesheets. Note: embedded stylesheets must be repeated on every page.

    - Using @import "CSS file" is terrible for performance.

#### Chapter 2: Core Concepts in CSS, Part 1

- Browsers apply **`Default Styles`**, but you can override them.
    - **Proximity** is one factor in style application.
        - The second declaration will override the first if we have two equal selectors.
        - The same is true if you have a single declaration block containing two of the same declaration.
        - Proximity applies to both linked and embedded stylesheets.
        - It also applies to the combination of embedded and linked. Linked stylesheets are external and, therefore, farther away from an embedded stylesheet. So the embedded one will override the external one.
    - HTML Markup forms a DOM tree.
        - ![chrome_EJ5s17qP9n](G:\My Drive\Education\Courses\modern-web-design\lesson-4\doc\lesson-4-notes.assets\chrome_EJ5s17qP9n.png)
        - Specificity is higher than proximity.
    - Debugging proximity and specificity
        - Use `!important`to verify whether specificity is why a declaration isn't being applied. Do not use this in your production stylesheets.
        - Dev Tools can show what markup is being overridden.

#### Chapter 3: Core Concepts in CSS, Part 2

- **Fault Tolerance** is how browsers handle errors.

    - Parsing errors happen. `p { color: red; }`

        - This ruleset presents three potential locations for parsing errors to occur.

            - The selector, the property, and the value.

            - ```css
                p {
                	color: red;
                	font-weight: bold;
                }
                ```

                - This declaration has **five** potential locations for parsing errors: the selector and two each of properties and values.

        - Knowing how parsing errors work lets us use modern CSS and provide fallbacks for older browsers.

            - ```css
                p {
                	background: #ccc; /* no RGBa */
                	background: rgba(0,0,0,.5); /* RGBa */
                }
                ```

            - A browser that understands RGBa will override the non-RGBa declaration.

        - You can also hide groups of declarations. Unfortunately, this ruleset is thrown away by browsers that don't support *attribute selectors*.

            - ```CSS
                html[lang] p {
                	background: #ccc; /* no RGBa */
                	background: rgba(0,0,0,.5); /* RGBa */
                }
                ```

        - You can also hide groups of rulesets. Browsers without *media query* support would ignore these.

            - ```css
                @media only screen and (min-width: 20em) {
                	p {
                		background: rgba( 0,0,0,.5);
                	}
                	ul {
                		background: rgba( 255, 255, 255, .5);
                	}
                }Allows you to create different experiences for different browsers.
                ```

        - The *attribute selector* was used to apply the advanced design only in more modern browsers.

            - ```css
                #intro {
                	/* Basic layout */
                }
                
                body[id=css-zen-garden] #intro {
                	/* Advanced layout */
                }
                ```

            - ```css
                <head>
                	<meta charset="utf-8" />
                	<title>Page Title</title>
                	<link rel="stylesheet" href="/c/basic.css">
                	<link rel="stylesheet" href="/c/advanced.css"
                		media="only screen and (min-width: 20em)">
                </head>
                ```

                - This same concept is how we achieve a "mobile first" design and deliver smaller files to less-capable browsers.

- Descendants **inherit** some CSS properties.

    - ![chrome_ns6zRJp2M1](G:\My Drive\Education\Courses\modern-web-design\lesson-4\doc\lesson-4-notes.assets\chrome_ns6zRJp2M1.png)

#### Chapter 4: Selecting Elements to Style, Part 1

- **Universal Selector**: Selects everything and is denoted by `*`.

- **Type Selectors**: Selects elements by name. (May also be referred to as *element selectors*)

    ```css
    p {
    	background: red;
    }
    
    ul {
    	background: green;
    }
    ```

- **Class Selectors**: Selects based on the class attribute of an element

    ```html
    <li class="first">Article I: Legislative Branch</li>
    <li class>Article II: Executive Branch</li>
    <li class="last">Article III: Judicial Branch</li>
    ```

    - ```css
        li {
        	background: blue;
        }
        .first {
            background: green;
        }
        .last {
            background: red;
        }
        ```

- **ID Selectors**: Select based on the ID attribute

    ```html
    <div id="content">
    	... Some Content ...
    </div>
    ```

    - ```css
        #content {
        	background: red;
        }
        ```

#### Chapter 5: Selecting Elements to Style, Part 2

- Testing for the existence of an attribute: 

    ```css
    // This would select any element with an alt attribute
    [alt] {
    	outline: 5px solid red;
    }
    ```

- This would select any element with an `alt` attribute whose value is "Aquent". 

    ```css
    [alt=Aquent] {
    	outline: 5px solid red;
    }
    ```

    - The match needs to be exact and case-sensitive.

- This would select any element with an `alt` attribute whose value contains the word "Aquent"

    ```css
    [alt~=Aquent] {
    	outline: 5px solid red;
    }
    ```

- This would select any element with an alt attribute whos value is "Aquent" or "Aquent-*".  

    ```css
    [alt|=Aquent] {
    	outline: 5px solid red;
    }
    ```

- Using the carat would select any element with an alt attribute whose value starts with "Aquent" 

    ```css
    [alt^=Aquent] {
    	outline: 5px solid red;
    }
    ```

- Using the dollar sign would select any element with an alt attribute whose value ends with "Aquent" 

    ```css
    [alt$=Aquent] {
    	outline: 5px solid red;
    }
    ```

- Using the asterisk would select any element with an alt attribute whose value contains "Aquent", even as part of another word. 

    ```css
    [alt*=Aquent] {
    	outline: 5px solid red;
    }
    ```

- Some selectors are equivalent, but not equal.

    - These are equivalent, but the attribute selector is less specific: 

        ```css
        #content {
        	background: red;
        }
        
        [id=content] {
        	background: red;
        }
        ```

- **Psuedo-Element Selectors** are for parts of the document

    - ```css
        /* These are dynamic too */
        ::first-letter {
            /* Rules applying to only the first letter
            	in the content of a block element */
        }
        ::first-line {
            /* Rules applying to only the first line
            	of content in a block element */
        }
        ::selection {
            /* Rules applying to any content selected 
            	by a user (such as when copying) */
        }
        
        /* We can enlarge the first letter of paragraphs */
        p::first-letter {
        	font-size: 20em;
        }
        ```

#### Chapter 6: Selecting Elements to Style, Part 3

- Pseudo-Classes target via context or properties.

    - ```css
        :hover {
        	background: red;
        }
        
        :focus {
        	background: blue;
        }
        
        :active {
        	background: green;
        }
        ```

        - In most cases, you want to apply the same styles on focus and hover. So that covers users whether they are using a mouse or keyboard.

    - ```css
        :target {
        	background: red;
        }
        ```

        - This selects an element that has been targeted using an anchor link

    - Other examples of pseudo-classes we have available to us: 

        ```css
        :first-child {
        	background: red;
        }
        
        :last-child {
        	background: blue;
        }
        
        :only-child {
        	background: green;
        }
        ```

        - These select based on source order with respect to their ~~siblings~~.

    - What would happen if we removed the `:only child` element? 

        ```css
        :first-child {
        	/*background: red;*/
        }
        
        :last-child {
            background: blue;
        }
        ```

        - Only children are both first and last children, so both selectors would match, but `:last-child` would apply.
        - When the selectors are equal, proximity wins.

    - You can select specific sibling groups using `:nth-child`. 

        ```css
        :nth-child(odd) {
        	background: blue;
        }
        
        :nth-child(even) {
        	background: green;
        }
        ```

    - Or specific siblings: 

        ```css
        :nth-child(1) {
        	background: blue;
        }
        
        :nth-child(15) {
        	background: green;
        }
        ```

    - Or you can select based on a formula. 

        ```css
        :nth-child(3n+3) {
        	background: blue;
        }
        ```

        - For every group of 3, pick the third one.

    - For every group of 10 siblings, select the 9th one. (9, 19, 29, etc). 

        ```
        :nth-child(10n-1) {
        	background: red;
        }
        ```

    - For every group of 7, assign a different color to each one. (Rainbow). 

        ```css
        :nth-child(7n+1) { color: red;		}
        :nth-child(7n+2) { color: orange;	}
        :nth-child(7n+3) { color: yellow;	}
        :nth-child(7n+4) { color: green;	}
        :nth-child(7n+5) { color: blue;		}
        :nth-child(7n+6) { color: indigo;	}
        :nth-child(7n+7) { color: violet;	}
        ```

    - You can select specific siblings based on **position** and the **element type**. 

        ```css
        :first-of-type {
        	background: red;
        }
        
        :last-of-type {
        	background: blue;
        }
        
        :only-of-type {
        	background: green;
        }
        
        :nth-of-type {
            background: yellow;
        }
        ```

    - You can also select based on contents. This would select any element with no children or text content: 

        ```css
        :empty {
            background: red;
        }
        ```

- **Special Pseudo-class for Inverting**

    - This selects any image with no `alt` attribute. 

        ```css
        img:not([alt]) {
        	outline: 5px solid red;
        }
        ```

#### Chapter 7: Selecting Elements to Style, Part 4

- Selectors can be combined for greater **specificity**.

    - Here we are selecting a `div` with an `id` of "content" and two `li` elements, each with a `class` of  "first" and "last". 

        ```css
        div#content {
            background: red;
        }
        
        li.first {
            background: green;
        }
        
        li.last {
            background: blue;
        }
        ```

        - Specificity is cumulative.

    - **Calculating Specificity**

        - ![soffice.bin_CTIAKK0rwo](G:\My Drive\Education\Courses\modern-web-design\lesson-4\doc\lesson-4-notes.assets\soffice.bin_CTIAKK0rwo.png) 
        - ![chrome_q08hrkAbg2](G:\My Drive\Education\Courses\modern-web-design\lesson-4\doc\lesson-4-notes.assets\chrome_q08hrkAbg2.png) 

    - **Descendant Selectors** select via ancestors

        - The space indicates descendants: 

            ```css
            #content p {
            	background: red;
            }
            
            div#content ul li.last {
            	background: blue;
            }
            ```

    - Child Selectors select based on a parent 

        ```css
        #content > p {
            background: red;
        }
        
        #content > li.last {
            background: blue;
        }
        ```

        - The greater symbol means the element on the right must be a child of the element on the left.

        - The second one doesn't apply: 

            ```html
            <body>
            	<div id="content">
                    <h1>This is a title</h1>
                    <p>This a <a href="#">link</a></p>
                    <ul>
                        <li class="first">This is the firest item</li>
                        <li>This is the second item</li>
                        <li class="last">This is the last item</li>
                    </ul>
                    <p>This is another parapgraph</p>
                </div>
            </body>
            ```

            - Because the list item classified as "last" is not a child of an element with the id of "content", it's a grandchild.

            - If we want to use the child selector, we need to include the parent, a ul, which is a descendent of "content". 

                ```css
                #content ul > li.last {
                	background: blue;
                }
                ```

####  Chapter 8: Selecting Elements to Style, Part 5

- The **Adjacent Sibling** selector is based on the previous sibling. 

    - The plus symbol means the element on the right must be a sibling of and adjacent to the element on the left. 

        ```css
        h1 + p {
        	background: blue;
        }
        li + li {
        	background: red;
        }
        ```

- The **General Sibling** selector is based on a previous sibling.

    - The tilde symbol means the element on the right must be a sibling of and follow the element on the left. 

        ```css
        h1 ~ p {
        	background: blue;
        }
        
        li ~ li {
        	background: red;
        }
        ```

- These are called **Combinators** and do not affect selector specificity.

#### Chapter 9: Controlling Typographic Styles

- CSS offers a variety of ways to control font display on a page.

    - **font-family** accepts a **font-stack**, a comma-separated list of acceptable font names in order from first choice to last.  

        ```css
        p {
            font-family: "Helvetica Neue", Arial, sans-serif;
        }
        ```

    - **font-size** can be set in various values from pixels to ems to inches to picas. Some are flexible; others are fixed. 

        ```css
        p {
            font-family: "Helvetica Neue", Arial, sans-serif;
            font-size: 2em;
        }
        ```

        - An em-based unit is always sized according to its context.
            - HOW EMS WORK:
                - .75em = context * 75%
                - 1em = context * 100%.
                - 2em = context * 200%.
                - 2.5em = context * 250%
                - The browser default for font context is 16px
                    - .75em = 16 * .75 = 12px.
                    - 1em = 16 * 1 = 16px.
                    - 2em = 16 * 2 = 32px.
                    - 2.5em = 16 * 2.5 = 40px.

    - **line-height** is not leading. Leading has space between the lines. The line-height has equal space on top and bottom.

        ```css
        p {
            font-family: "Helvetica Neue", Arial, sans-serif;
            font-size: 2em;
            line-height: 1.5;
        }
        ```

        - Unitless line heights are preferred.

    - **font-weight** lets you control the heaviness of the glyphs 

        ```css
        p {
            font-family: "Helvetica Neue", Arial, sans-serif;
            font-size: 2em;
            line-height: 1.5;
            font-weight: bold;
        }
        ```

        - font-weight can be bold, normal, or a specific size 

            ```css
            p {
                font-weight: bold;
                font-weight: normal;
                font-weight: 600;
            }
            ```

    - **font-style** and **font-variant**

        ```css
        font-style: italic;
        font-variant: small-caps;
        ```

    - All of these properties can be rolled up into a single declaration for brevity 

        ```css
        p {
            font: 	italic 		/* style (optional) */
                	bold		/* weight (optional) */
                	small-caps	/* variant (optional) */
        			2em/1.5		/* size / line-height */
                				/* font */
                	"Helvetica Neue", Arial, sans-serif; 
        }
        ```

    - Properties that aren't included in a rollup

        - **text-transform** is adjusting the case of text (uppercase, lowercase, etc). 

            ```css
            p {
                font: 	italic 		/* style (optional) */
                    	bold		/* weight (optional) */
                    	small-caps	/* variant (optional) */
            			2em/1.5		/* size / line-height */
                    				/* font */
                    	"Helvetica Neue", Arial, sans-serif; 
            	text-transform: uppercase;
            }
            ```

        - **text-decoration** is typically seen in the context of whether anchors have an underline. 

            ```css
            a {
            	text-decoration: underline;
            }
            ```

            - underline, overline, line-through
            - word-spacing, letter-spacing

        - **font-smoothing** tweaks the letterforms for a crisper appearance. 

            ```css
            p {
                	-moz-font-smoothing: antialiased;
                	 -ms-font-smoothing: antialiased;
                 -webkit-font-smoothing: antialiased;
                		 font-smoothing: antialiased;
            }
            ```

            - Unfortunately, this is a property that requires prefixing for use in certain browsers.

- You can control how the content aligns and flows

    - **white-space** controls whether the content can wrap to a new line. 

        ```css
        a[href^=tel] {
        	white-space: nowrap;  /* Telephone numbers do not wrap to new lines.
        }
        ```

    - **text-align** control how text fills the container. 

        ```css
        p {
        	text-align: justify;
            text-indent: 1em
        }
        ```

        - Justify generally looks bad on the web, but you can also align left, right, and center.

#### Chapter 10: Custom Fonts

- Sometimes referred to as web-fonts. It means you can define custom typefaces.

    - ​	The `@font-face` block lets you define a custom font. Then, use the font name in your font-stack.

        ```css
        @font-face {
            font-family: Arnhem;
            src: url(/c/f/ArnhemPro-Normal.woff) format("woff"),
                 url(/c/f/ArnhemPro-Normal.ttf) format("truetype");
            font-weight: 400;
            font-style: normal;
        }
        
        /* Elsewhere in the stylesheet */
        p {
            font-family: Arnhem, Georgia, serif;
        }
        ```


##### Assignment 7

- **Steps**
    - Return to your site, create a new text file, and save it as main.css.
    - Use the link element and include it on each page of your site inside the head element.
    - Return to your main.css file and insert a simple rule set: `body { color: red; }`. Then save the file and check that it the rule is being applied to your pages. If it is, move on; if not, check your link syntax.
    - Delete the sample rule set, but use this CSS file in subsequent assignments for all your CSS work.
- **Thoughts**
    - Think about the way the browser styles the text content of your documents.
    - Are your pages easy to scan and comfortable to read?
    - How could you use typography to improve readability and enforce content hierarchy and importance?
    - How do different font families look when paired with each other?
    - Test out some different font stacks and note how fallbacks differ.
    - Publish your work to GitHub and post a link in the forum along with your observations regarding working with type in CSS.

#### Chapter 11: Color in CSS

- Color can actually take many forms in style sheets. The most common one we’ve seen is using color keywords. That’s the most simplest and straightforward.

    - There are over 140 different color keywords. You probably will never remember them all. But they can be useful when you’re just trying to comp something up pretty quickly and you want red, green, what have you.

    - For most projects however, those color keywords are only going to get you so far. You might be able to use them for white and black. But chances are you’re going to want to customize the colors a little bit more specifically for your project.

    - The first and most common color type that you’ll run into is **hexadecimal format**. It looks a little something like this. 

        ```css
        p {
        	color: #ff0000;
        }
        ```

        - Where you see a hash followed by Fs, zeros, numbers, and so on and so forth. Basically: `A through F` and `zero through nine`.

        - So hexadecimal is almost always six digits. Or in some cases, three, which I’ll show you in a minute. Each of those is broken down into pairs. So, in this case ff, 00, and 00. And each of those is assigned to a different color channel, which I’ll show in a moment.

        - Hexadecimal can be used to define colors with the red, green, and blue channels having values from 00 to ff.

        - If all three are double values, you can use a hexadecimal (hex) shorthand. 

            ```css
            p {
            	color: #f00;	/* #ff0000 = RRGGBB*/
            }
            ```

        - ```css
            p {
                color: rgb(255, 0, 0);		/* Fallback */
                color: rgba(255, 0, 0, .5); /* 50% transparency */
            }
            ```

            - So you’ll remember back to our fault tolerance discussion. That this would actually allow us to have a fallback for older browsers that don’t understand RGBA. They would get the RGB value, with the RGBA value being applied only in browsers and understand it.

    - If you’re a designer who tends to think more in hues, HSL is another color option that lets you define the color based on hue, saturation, and lightness. 

        ```css
        p {
        	hsl(0, 100%, 50%);
        }
        ```

        - With hue, saturation, and lightness, we’re dealing with the movement from black to white along the L, the lightness channel. With HSB, we’re adjusting the brightness.
        - So it’s a little bit different. If you go all the way up in the lightness, you will hit white. If you go all the way in the brightness, you end up with the truest representation of that particular color. 

#### Chapter 12: Working with Color

- The `color` property controls the foreground. Foreground refers to both the text color and the border color of an element. Foreground is an inherited value.

- The `background-color`applies to the background of an element. This property is not inherited.

    - If we assign a background of red to the document, you see that everything turns red. If I tree down into the div, however, you see that there is no background color inherited by that div. 

    - If, however, I change the background to being a foreground color of red, now all of a sudden, its color is red in the diagnostic tools there. But if I inspect the heading level, you’ll see that it has a color of red as well. Because that is inherited. Foreground color is inherited.  

        - ```css
            p {
            	background: #ccc;
                border: 1 px solid;
                box-shadow 3px 3px 3px #f90;
                color: #f99;
                text-shadow: -5px 5px 15px #fff;
            }
            ```

        - Here we have background, which is a shorthand for background color, background image. We’ll look at all of those properties later. But background, you could simply say, in this case, is a light gray.

        - The border is 1 pixel solid and that’s going to inherit the foreground color. We have a box shadow here that’s got a color. We have the foreground color. And we have a text shadow, also with a color. 

- Now, `text-shadow` can be used to give you a nice drop-shadowy effect on text. 

    ```css
    p {
        text-shadow: -5px	/* Horizontal offset */
            		  5px	/* Vertical offset */
            		 15px	/* Blur radius (optional) */
            		 #fff;	/* Color */
    }
    ```

    - So here you see text shadow has four properties—the horizontal offset; the vertical offset; how much of a blur you want, which is optional; and then the color that you want that text shadow to be. Here is that without the comments on it. So it’s not necessarily quite as long and scary looking. 

        ```css
        p {
        	text-shadow: -5px 5px 15px #fff;
        }
        ```

##### 	Assignment 8: Splash Some Color

- Return to your site and think about how color could improve the readability and usability of your pages. 
- Try out a couple of the different forms using hex, using RGB, HSL. 
    - What feels more natural to you? 
    - Do you find pros and cons working in each of them?
- Now look at your site. 
    - Does it have enough contrast? 
    - There is a grayscale plugin for Chrome that you can download to actually see if the colors you’ve chosen give you enough contrast when you view it in grayscale. This can be helpful for mimicking what it looks like if you have a form of color blindness.
    - Publish your work on GitHub, and post a link in the forum, along with your observations regarding working with color in CSS.

#### Chapter 13: Controlling an Element's Dimensions, Part 1

- 