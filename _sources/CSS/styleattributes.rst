Changing the Style of an HTML Element
=====================================

There are many ways that we can change the style of what we see in the browser.  In this section we will look at examples of the following:

* background
* text
* font

But before we talk about these, we need to think about colors.  There are three different ways to specify the color.

* by name, like blue, red, green.  You can see a complete list of `color names <http://www.w3schools.com/cssref/css_colors.asp>`_ on the w3schools website.
* using an RGB value like ``rgb(255,0,0)``
* using a HEX value like ``#ff0000``

Using either the RGB or the HEX value gives you total control to specify any of of 16 million different colors.  There is a bit of interesting computer science behind the RGB and HEX values.  The rgb function lets you specify a value between 0 and 255 for each component of red, green, and blue.  By mixing together a certain amount of red, green, and blue you can create :math:`255 \cdot 255 \cdot 255` different colors, which is slightly more than 16.5 million.  Now where does the number 255 come from?  It is one less than :math:`2^8`.  Computer scientists like powers of two because when you get deeply into the inner workings of the computer you see that everything is in binary (ones or zeros) which we call bits.  With eight bits we can specify 256 different values or 0 -- 255.  We call eight bits one byte.

Now the HEX specification of the number is directly related to the binary as follows:

======  ===  =======
binary  hex  decimal
======  ===  =======
0000     0   0
0001     1   1
0010     2   2
0011     3   3
0100     4   4
0101     5   5
0110     6   6
0111     7   7
1000     8   8
1001     9   9
1010     a   10
1011     b   11
1100     c   12
1101     d   13
1110     e   14
1111     f   15
======  ===  =======

When specifying a color using the HEX system the first two characters are for the red, the second two for the green, and the last are for the blue.  There are lots of color picking tools that you can use that will let you choose the color you want and then tell you the appropriate hex value.


Background
----------

CSS has the following properties which we can use to change the background.

* background-color
* background-image
* background-repeat
* background-attachment
* background-position

.. activecode:: css_bkgrd_1
   :language: html

   <html>
      <head>
         <style>
         h1 {
            color: blue;
            font-size: 28pt;
         }
         body {
             background-image: url("http://m.99wallpaper.com/images/7_1306/Black%20Background%20Wood%20-%202560x1600%20by%20Freeman.jpg")
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


Text
----

* text-color
* text-align
* text-decoration
* text-transformation

Font
----

* font-family
* font-style
* font-size
