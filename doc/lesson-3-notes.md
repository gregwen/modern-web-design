### Lesson 3: Getting Started with CSS

[TOC]

#### Chapter 1: Simple Flow Level Semantics

- **Paragraphs** should be contained in `p` elements. They break up the text to make it easier to read.

    - ```html
        <p>Since the constitution was ratified in 1789, it has been amended 27 times. The first ten amendments, known collectively as the Bill of Rights, offer specific protections of individual liberty and justice and place restrictions on the powers of government within the U.S. states. The majority of the 17 later amendments expand individual civil rights protections. Others address issues related to federal authority or modify government processes and procedures. Amendments to the United States Constitution, unlike ones made to many constitutions worldwide, are appended to the document.</p>
        
        <p>The original U.S. Constitution was written on five pages of parchment. The first permanent constitution, it is interpreted, supplemented, and implemented by a large body of federal constitutional law and has influenced the constitutions of other nations.</p>
        ```

- HTML contains multiple types of **lists**

    - `ol` (**Ordered** Lists) and `ul` (**Unordered** Lists) make use of the `li` (List-Item) element.

        - ```html
            <li class="list">Article I: Legislative Branch</li>
            <li class="list">Article II: Executive Branch</li>
            <li class="list">Article III: Judicial Branch</li>
            ```

        - If the order of the list matters, the list should be inside an `ol` element. (Numbers)

        - If the order does not matter, the list should reside inside a `ul` element. (Bullets)

    - **Description** Lists

        - Description lists have a special setup. Usually used for something like a glossary. (Terms and Definitions)

        - Terms are wrapped in `dt` elements.

        - Definitions are wrapped in `dd` elements.

        - The whole thing gets wrapped in a `dl` element.

        - ```html
            <dl>
            	<dt>Article I</dt>
            	<dd>Article I describes Congress, the federal government's legislative branch. Section 1 reads, "All legislative powers herein granted shall be vested in a Congress of the United States, which shall consist of a Senate and House of Representatives."</dd>
            </dl>
            ```

        - Description lists can contain a single or multiple items.

- **Heading Levels**

    - H1(most important headline on a page) → H6 (least important headline on a page)

- **HR**

    - Sometimes you need a line break `<hr>`
        - Previously, `hr` was a horizontal rule, a simple line in the html text.
        - It has been recast as a paragraph-level thematic break. 
        - They are used for shifts of a subject, location, etc.

#### Chapter 2: Dealing with Data

- When displaying tabular data, using the **table** element is the right choice.

    - ```html
        <table>
            <tr>
                <td>Title</td>
                <td>Price</td>
                <td>Available</td>
            </tr>
            <tr>
                <td>CSS Demystified</td>
                <td>$29</td>
                <td>16</td>
            </tr>
            <tr>
                <td>Mastering JavaScript</td>
                <td>$35</td>
                <td>10</td>
            </tr>
            <tr>
                <td>HTML5: An Introduction</td>
                <td>$15</td>
                <td>6</td>
            </tr>
        </table>
        ```

    - The `table` element must contain **rows** (`tr`) and **cells** (`td`).

    - Good tables contain **captions** (`caption`), **table header blocks** (`thead`) and **table body blocks** (`tbody`).

        - ```html
            <table>
            	<caption>Text about this table</caption>
            	<thead>
            		<!-- rows & columns with th -->
                </thead>
                <tbody>
                    <!-- rows and columns with tr/td -->
                </tbody>
            </table>
            ```

    - Some tables contain footers (`tfoot`), which should appear above the table body blocks (`tbody`).

        - ```html
            <table>
            	<caption>Text about this table</caption>
            	<thead>
            		<!-- rows & columns with th -->
                </thead>
                <tfoot>
                    <!-- can also contain multiple rows and columns. Despite its location in the code, this is a footer for the table. -->
                </tfoot>
                <tbody>
                    <!-- rows and columns with tr/td -->
                </tbody>
            </table>
            ```

    - A table can have multiple body blocks. 

    - In the `thead`, table header cells (`th`) can be used for header info and should be **scoped** `<th scope="column">` to a column.

    - The `scope` element allows us to define the direction in which the table header is scoped. For example, inside a table body, it might be scoped into a row.

#### Chapter 3: Complex Flow Level Semantics

- Long quotes or excerpts belong in a **Blockquote** (`<blockquote>`).

    - Indicates that a chunk of content is quoted from another source.
    - The blockquote element must contain other flow-level elements like `p`, `ul`, `ol`, headings, tables, etc.
    - By default, browsers will indent blockquotes. We can control that using CSS.
    - We can use the **cite** `<blockquote cite="//some-source-website-url">` attribute to indicate the source. Unfortunately, most browsers do not expose this information to the user, but you can do this with javascript.

- We can reference content within our own pages. For this, we use the **figure** (`<figure>...</figure>`) element.

    - The figure element can contain images, tables, charts, or anything else that could exist independently.
    - As the purpose of a figure is to create a reference-able element, you should put unique id attributes on them.
    - The figure element can contain a caption (`figcaption`) which can, in turn, contain other elements.  Captions provide more context.

- The details and summary elements make an **Accordion**.

    - Accordions are content that is expandable and collapsible.

    - When the browser displays this, only the `summary` is visible until you click it.

        - ```html
            <details>
                <summary>Much like a title or one-liner</summary>
                <p>
                    Some text here gives more details and context.
                </p>
            </details>
            ```

        - Clicking the summary will cause the content to expand and reveal the details.

#### Chapter 4: Organizational Semantics

- **DIV** creates generic divisions

    - No semantic value to a div element.
    - Often has a class or id associated with giving it more meaning to the author.
    - This element should be used sparingly.

- The **Main** element should be used to indicate the main body of the page, the page's focal content.

    - ```html
        <body>
        	<main>
        		<h1>Some header text</h1>
        		<p>Some content</p>
        	</main>
        </body>
        ```

- Within the main content, we may need to subdivide the content into chunks.  The element we use is the **section** element.

    - Sections contain all the content (paragraphs, images, etc.) related to a topic.

        - ```html
            <body>
            	<main>
            		<h1>Some header text</h1>
            		<p>Some content</p>
                    <section id="article-1">
                        <h2>Some header text</h2>
            			<p>Some content</p>
                        ...
                    </section>
                    ...
            	</main>
            </body>
            ```

- **Articles** are like autonomous `sections`.

    - A simple test: an `article` is for contents that could be removed without affecting their meaning or the meaning of the page.

        - ```html
            <body>
            	<main>
            		<h1>Some header text</h1>
            		<article>
            			<h2>Some heading</h2>
            			<p>Some content</p>
            		</article>
            		<article>
            			<h2>Some heading</h2>
            			<p>Some content</p>
            		</article>
            		<article>
            			<h2>Some heading</h2>
            			<p>Some content</p>
            		</article>
            	</main>
            </body>
            ```

        - Think of them like an article of clothing. Take it off a person or put it on, but neither defines the other.

- **HTML5 Element Flowchart**

    - ![chrome_5pQIA9op43](G:\My Drive\Education\Courses\modern-web-design\website\lesson-3\doc\lesson-3-notes.assets\chrome_5pQIA9op43.png)

- An **aside** is used for tangentially related content.

    - Tangentially:  *in a way that relates only slightly to a matter; peripherally.*

    - ```html
        <body>
        	<main>
        		<h1>Some header text</h1>
        		<article>...</article>
        		<article>...</article>
        		<article>...</article>
                
                <aside>
                    <h1>Links</h1>
                    <ul>
                        <li></li>
                        <li></li>
                        <li></li>
                        <li></li>
                    </ul>
                </aside>
        	</main>
        </body>
        ```

    - Something like a sidebar. Beneficial, but not necessary.

#### Chapter 5: More Organizational Semantics

- The **NAV** element should wrap up your navigation.

    - The nav element can contain many other elements.

    - ```html
        <nav>
            <h1>Some header</h1>
            <ul>
                <li>Article I: Legislative Branch</li>
                <li>Article II: Executive Branch</li>
                <li>Article III: Judicial Branch</li>
                ...
            </ul>
        </nav>
        ```

    - Lists make excellent link containers.

- The **Header** element is for intro content.

    - ```html
        <body>
        	<header>
        		<h1><a href="#">Some header/title</a></h1>
        		<a href="#menu">Jump to Menu</a>
        	</header>
        	<main>
        		...
        	</main>
        </body>
        ```

    - This is an example of the header element in use as the site's banner.

- The **Footer** is for meta info concerning the content.

    - This is an example of a footer element containing copyright and licensing information.

    - ```html
        <footer role="contentinfo">
        	<p id="copyright">The text content of this site was borrowed from <a href="#">the Wikipedia article on the U.S. Constitution</a> on <time>22 January 2023</time> under the <a href="#">Creative Commons Attribution-ShareAlike License</a>.<br>Licensing terms of content from other sources (photos, etc.) is noted along with each respective resource.</p>
        </footer>
        ```

- **Standards Note:** Articles and sections can also contain a header and footer.

    - This article has some introductory content.

    - ```html
        <article>
            <header>
                <h1>Title of article</h1>
            </header>
            <p>Some article content</p>
            ...
        </article>
        ```

- The **Role** attribute states an element's purpose.

    - It is part of the **WAI-ARIA** (Web Accessibility Initiative – Accessible Rich Internet Applications) specification.

        - a technical specification published by the *World Wide Web Consortium* that specifies how to increase the accessibility of the web.

    - Aria defines a number of roles, such as the role of the `bannerThe.

        - A role of "**banner**" defines this header as the site banner.

            - ```html
                <header role="banner">
                    <h1>Some header</h1>
                </header>
                ```

        - A role of "**contentinfo**" defines this footer as containing meta information for the page as a whole.

            - ```html
                <footer role="contentinfo">
                    <p>some copyright content</p>
                </footer>
                ```

        - We also have roles of navigation, search, and various other ones.

            - Navigation looks redundant on a `nav` element: `<nav role="navigation">`
            - The redundancy exists because HTML5 and ARIA evolved to solve some of the same problems.
            - Over time this redundancy will become less necessary.

        - The first header child of the body is given an inferred `banner` role, and the footer gets `contentinfo`.

#### Lesson 3: Assignments

- **Assignment 5:** Take Quiz #2.
    1. Which element represents self-contained content, frequently with a caption `figure`
    2. Which element would you choose to markup a list where the order of the items matters? `ol`
    3. What is the meaning of the `hr` element? 
        A paragraph-level thematic break.
    4. How many heading elements are there in HTML?
        Six
    5. Which element pair creates a native accordion?
        `details/summary`
    6. Which HTML element should be used to indicate the primary content area on a page?
        `main`
    7. Which element is used for meta-information about the content of a page, article, or section?
        `footer`
    8. What is the `role` attribute used for?
        To indicate the function that the element is plays in the interface
    9. What does ARIA stand for?
        Accessible Rich Internet Applications
    10. Which `role` should be used for your website's header?
        `banner`
- **Assignment 6:** Go back to your HTML page and organize the page using the knowledge gained from this lesson.
    - Page: https://gregwen.github.io/website/lesson-three-assignment/
    - Repository: https://github.com/gregwen/website/tree/main/lesson-three-assignment