Changing your page layout
=========================

The CSS Box Model
-----------------

All HTML elements can be thought of simply as boxes.  In fact that is exactly how the browser thinks of them as it begins the process of rendering the page.  When doing web page design and layout it is very common to hear designers talk about the CSS box model.  Figure 1 illustrates the different components that go into the box model.

.. figure:: Figures/box-model.gif

   Figure used in accordance with w3schools fair use policy

The different parts of the box model are defined as follows:

* Content:  The actual text or image content of an html tag
* Padding:  The space between the content and the border.
* Border:  This can be an actual drawn border or it can be invisible
* Margin: The space outside the border between this box and the boxes next to it in each direction.

Lets try a simple example:

.. activecode:: css_ids
   :language: html

   <html>
      <head>
         <style>
         section {
              width: 250px;
              background-color: green;
              padding: 25px;
              border: 10px solid blue;
              margin: 25px;
              }
         </style>
       </head>
   <body>

      <section>Hello World</section>
      <section id=b>Hello World</section>

   </body>
   </html>

Positioning
-----------


Floating
--------
