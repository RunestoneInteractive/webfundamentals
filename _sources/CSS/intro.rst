Introduction to CSS
===================

CSS stands for Cascading Style Sheets.  Style sheets define how to display your html code.  This was not always the case.  In HTML 3 the designers of the language added tags like font and color. This was great for companies like Microsoft where you could export your word doc as html, but created a nightmare for developers of large sites that were not developed using WYSIWYG tools, and it made the html completely unreadable.  So, in HTML 4.0 CSS was introduced to fix the problem we created for ourselves.

CSS defines how the html should look, and it does this using a set of rules.  We are all used to following certain rules in every day life:  **If** it is raining, **then** take your umbrella.  **If** the light is red, **then** come to a stop at the stoplight.  In html terms we might say, **if** the tag is an ``h1`` **then** color it blue and set the font size to 28 points.

CSS Syntax
----------

To tell the computer about these if/then rules, we need a consistent syntax.  The syntax for CSS has two parts, a selector and a declaration.

.. code-block:: css

   selector {
       declaration;
       declaration;
       }

The declaration itself consists of two parts: a property and a value.  There are many many CSS properties and we willl look at a lot of them, but for now, just think of the property as something like color, font-size, font-family, etc.

Selectors can be as simple as a tag name, or a very complex pattern to match.  We will start with some very simple selectors and work our way up to the more complex.

Without further fuss, lets look at a CSS rule for coloring h1 tags blue, and changing their font to 28 points.

.. code-block:: css

   h1 {
       color: blue;
       font-size: 28pt;
   }


Including CSS in Your Page
--------------------------

There are three ways to include CSS in your html document.

* You can add a style attribute to a tag.  This should not be used very often, if ever!
* You can embed your CSS in your file inside a ``style`` tag.  We'll use this method in this book for convenience.
* You can put all of your CSS in a separate style file and include the style file into your HTML.  This is the preferred way of doing it because it achieves the greatest amount of separation between the content and how the content looks.

Lets now look at a complete example:

.. activecode:: css_rule_1
   :language: html

   <html>
      <head>
         <style>
         h1 {
            color: blue;
            font-size: 28pt;
         }
         </style>
      </head>
      <body>
         <h1>Hello World!!</h1>
         <p>The paragraph text should be unchanged</p>
         <h2>I am not blue!</h2>
         <h1>Hello Again</h1>
      </body>
   </html>


There are several things to notice about the example above.  First the ``h1`` selector matches all of the h1 tags in the document.  But it does not match the ``h2`` or the ``p`` tags.  If you want to change the style of the paragraph you need to add another rule.  Lets try it:  Add a rule to the style tag that colors the paragraph text green.  Then make another rule that makes the h2 tag size 16pt and yellow.

One thing to be careful about is to remember the semi-colons after the values.  If you forget a semi-colon, then your rule will not work.
