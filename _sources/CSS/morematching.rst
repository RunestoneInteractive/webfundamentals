More on Matching
================

Now that we know how to change some style elements on tags we can move on and learn more about selectors and how to use selectors in conjunction with two new html attributes that give us a lot more flexibility in styling an html document.


Matching multiple tags
----------------------

suppose we want to have h1, h2, and h3 headers in blue, but h4, h5, and h6 headers in green?  We do not have to write a separate rule for each header tag, we can write one rule that looks like this:

.. code-block:: css

   h1,h2,h3 {
       color: blue;
   }

   h4,h5,h6 {
       color: green;
   }


You can read the commas between the tags as "or."  So the first of the above rules read as If the tag is h1 or h2 or h3 then change the color to blue.

In the example below, add a rule so that the h2 and the paragraph have the color red.

.. activecode:: css_or
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


Using an id attribute in a rule
-------------------------------

Another common situation is that you have one particular paragraph that you want to have in a different color.  You cannot just use a selector that matches the p tag as that will match all of the p tags.  So in this case we need to somehow mark a particular paragraph so that we can have a selector that selects that paragraph and only that paragraph.  This is where the ``id`` attribute is used.    Any html tag can have an id attribute, which serves as a **unique identifier** for that tag.  In fact, the value of the id attribute must be unique throughout the file.


In the example below we have two rules.  One that changes the text to blue in all paragraphs.  The second rule changes the font-size to 18pt for the paragraph that has the identifier of "abc456"  The hashtag ``#`` is very important to this rule as it tells the css matcher that what comes after that hashtag must match the id attribute of some element.  So, in fact the p is redundant in this example, and you could remove the p from the beginning of the selector and the rule would still work.  In fact, you should try that now.

.. activecode:: css_ids
   :language: html

   <html>
      <head>
         <style>
         p {
            color: blue;
         }
         p#abc456 {
            font-size: 18pt;
         }
         </style>
      </head>
      <body>
         <h1>Hello World!!</h1>
         <p id="xyz123">The paragraph text should be unchanged</p>
         <h2>I am not blue!</h2>
         <h1>Hello Again</h1>
         <p id="abc456">This is another paragraph with a different identifier.</p>
      </body>
   </html>


What do you think will happen if you change the second rule so that it sets the color to red?   If you said that it will keep the first paragraph's color blue but change the second to red, your are correct.  Why does the second rule over-rule the first?  Because the second rule is more specific.  You might have thought it was because of the order of the rules, but in fact you can change the order of the two rules and try it and you will see that you still get the same result.

Using the class attribute in a rule
-----------------------------------

Sometimes you want to match some elements that are the same tag but not others.  One example of this is when you want to have a "zebra striped" table, where every other line has a slightly different background color then you are going to want to use a ``class`` attribute.  Classes and CSS may be the single most useful combination for styling your web pages.

Unlike the ``id`` attribute, many different tags can have the same value for a class.  Some examples:

You have paragraphs or headings and you want some normal, some are "warnings", some are "errors", and some are "cautions".   Or perhaps you have a list of things, some things one the list are hight priority, some are low, and some are medium.  By using a class you can apply a consistent style to all of the things that belong to that class (have the same value for their class attribute.)

To select any element that matches a particular class you use the ``.`` before the name of the class.  So ``.high`` will match any tags that have the attribute ``class=high``.

Returning to our HTML table example we have some rows that are "odd" and some that are "even".  Let's make a short table and style the odd and even rows differently.

.. activecode:: css_classes
   :language: html

   <html>
      <head>
         <style>
         .odd {
            background-color: #9999ee;
         }
         .even {
            background-color: pink;
         }
         </style>
      </head>
      <body>
           <table>
           <tr class="odd"><td>aapl</td><td>$101.23</td></tr>
           <tr class="even"><td>goog</td><td>$583.10</td></tr>
           <tr class="odd"><td>tsla</td><td>$281.10</td></tr>
           <tr class="even"><td>amzn</td><td>$331.33</td></tr>
           </table>
      </body>
   </html>



Now for some additional practice let's make the table look really nice.  Add a header and have the background of the header be light gray.  Make the text of the header bold and slightly larger.  Overall change the table so its width is 50% of the page and get rid of the page. `This page <http://www.w3schools.com/css/css_table.asp>`_ gives you a complete rundown on how to style tables.


Matching Children
-----------------

When using the semantic html elements it is sometimes very desireable to match a particular tag, but only if that tag is in the article section.  CSS allows us to match tags that are descendants of other tags by using a space after the parent tag.  For example:

.. code-block:: css

   article h1 {
       color:  purple;
   }


Will change the color of the h1 but only if they are descendants of the article tag.


.. activecode:: css_descendant
   :language: html

   <html>
      <head>
         <style>
         article h1 {
             color: purple;
         }
         </style>
      </head>
      <body>
      <h1>This is outside the article</h1>
      <article>
          <h1>This is inside the article</h1>
          <section>
              <h1>This is in a section of an article</h1>
          </section>
      </article>
      </body>
   </html>


In the example above, both of the h1's inside the article were changed because they are both descendants of the article.  If we only wanted to change the h1 that is a direct child of the article we can replace the space with a ``>`` giving us ``article>h1`` which indicates that only the immediate child should have its style changed.
