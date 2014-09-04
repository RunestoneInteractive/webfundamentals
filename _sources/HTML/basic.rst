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

.. activecode:: html_img
   :language: html
    
   <p>This is a short sentence.</p>   
   <img src="small_me.jpg">
   <p>This is a paragraph.  What happens when we have a really really really long line that takes up more than one line of the browser? <p>
   <p>Level this is a short sentence</p>


