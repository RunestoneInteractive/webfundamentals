Basic HTML Tags
===============

Headings
--------

Like any document HTML documents may have several layers of headings.  In fact you can have heading levels from 1 to 6 in an HTML document.

.. activecode:: html_headings
   :language: html
   
   <h1>Level one</h1>
   <h2>Level two</h2>
   <h3>Level three</h3>
   
   
Now modify the example above to add the next three levels of headings.  What do you notice?  What happens if you add a level 7 heading?   What happens if you close an h2 tag with an h1 or an h3?

.. reveal:: reveal_heading

   As you might expect, the headings continue to get smaller as you go from 1 to 6.  But when you go to level 7 the text gets bigger.  This is because the web browser is written so that it just ignores any tags that it does not know about.  This is somewhat of a disadvantage as you don't get any error messages, things just look wrong, and you have to figure out why.
   
   
   
Another aspect of the heading tag is that it is what we call a **block** tag.  Notice that each heading appears on its own line.  Thats pretty much what we would expect for a heading.  But not necessarily for other tags.  shortly, we will see some **inline** tags that do not each appear on their own line.


Paragraphs
----------

Paragraphs are another funamental element of documents.  Paragraphs are also another example of a block element in that each paragraph gets its own space and is separated from other html elements by blank lines in the document.


.. activecode:: html_paragraph
   :language: html

   <p>This is a short sentence.</p>   
   <p>This is a paragraph.  What happens when we have a really really really long line that takes up more than one line of the browser? <p>
   <p>Level this is a short sentence</p>


What happens when you put a paragraph inside another paragraph?  What about a header inside a paragraph?


Images
------

Images are another common element of a document or a web page.  To include an image in a document you must use an ``img`` tag.  Image tags are an example of an **inline** element because they just flow in with the surrounding text.  They do not force a new block to be created in the rendering of the html.  Here are a couple of images:

.. figure:: Figures/LutherBellPic.jpg

   Luther Bell:  ``http://interactivepython.org/runestone/static/webfundamentals/_static/LutherBellPic.jpg``

.. figure:: Figures/norse-logo.png

   Norse Logo:  ``http://interactivepython.org/runestone/static/webfundamentals/_static/norse-logo.jpg``


The image tag has a new component to it called an attribute.  In general tags can have many attributes in the case of an image we can inlude it by using a ``src`` attribute that contains the URL to the image we want to embed.  We can embed any image on the internet in our own document by referring to it by its URL in the ``src`` attribute.

.. activecode:: html_img
   :language: html
    
   <h1>Embedded Images</h1>
   <p>Images are inline elements they fit in the flow
   <img src="http://interactivepython.org/runestone/static/webfundamentals/_static/LutherBellPic.jpg">
   of a paragraph without causing extra line breaks.</p>
   

Try modifying the example above so that it includes the norse logo rather than the bell.  
You can also change the height and width of  an image by using a ``height=`` attribute or a ``width=`` attribute.  Try changing the size of the image in the example above.  Notice what it does to the flow.  Try changing just one of height or width and then try changing both at the same time.  You can stretch your image in all kinds of crazy ways.

There are several other attributes of the link tag as well.  You can read about them `here <http://www.w3schools.com/tags/tag_img.asp>`_.


Links
-----

The last basic link to cover in this section is the link tag ``a``.  In fact the last sentence of the previous section used a link to send you to the w3schools website to learn more about the attributes of an ``img`` tag.  Links are what made the web so popular in the first place.  Today we call them links, but in earlier years they were usually referred to as Hyperlinks. You can provide a link to any URL on the web using the ``href`` attribute on the ``a`` tag.   The text that you will click on goes between the opening ``a`` tag and the closing ``a`` tag.


.. activecode:: html_link
   :language: html
    
   <h1>Links make the web!</h1>
   <p>Links are another inline element.  You can read about links and their attributes
   <a href="http://www.w3schools.com/tags/tag_a.asp">Here</a> on the w3schools website.</p>


Try clicking on the link in the example above.  What happens?  How do you get back?   Don't worry, you can always just reload this page.
