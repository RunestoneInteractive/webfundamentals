Advanced HTML Tags
==================


Unordered Lists
---------------

.. activecode:: advhtml_ul
   :language: html

   <ul>
   <li>This is an unordered list</li>
   <li>The <code>li</code> tags come between two <code>ul</code> tags
   </ul>


Ordered Lists
-------------

.. activecode:: advhtml_ol
   :language: html

   <ol>
   <li>This is an ordered list</li>
   <li>The <code>li</code> tags come between two <code>ol</code> tags
   <li>Notice that the <code>li</code> tags are used for both.
   </ol>

The ``ol`` tag can also have a type attribute.  The type attribute can be one of the following values

* 1 This will cause the list to be numbered with numbers
* A This will cause the list to be ordered with upper case letters
* a This will cause the list to be ordered with lower case letters
* I This will cause the list to be ordered with upper case roman numerals
* i This will cause the list to be ordered with lower case roman numerals

Try it yourself.

Description Lists
-----------------

.. activecode:: advhtml_dl
   :language: html

   <dl>
   <dt>Description list</dt><dd>A list for defining terms</dd>
   <dt>dt</dt><dd>The <code>dt</code> tags are for the term</dd>
   <dt>dd</dt><dd>The <code>dd</code> tags are for the description</dd>
   </dl>

Nesting Lists
-------------

Lists can be inside of other lists. Too.  This is very much true of most HTML tags.

.. activecode:: advhtml_nested
   :language: html

   <ol>
   <li>This is an ordered list</li>
   <li>The <code>li</code> tags come between two <code>ol</code> tags
   <li>Notice that the <code>li</code> tags are used for both.
   <ul>
   <li>This is an unordered list</li>
   <li>The <code>li</code> tags come between two <code>ul</code> tags</li>
   </ul>
   <li>You can mix and match lists like this as deeply as you want.</li>
   </ol>


Tables
------

Tables have many uses, you can use them for organizing data as you normally would in a report where you have rows and columns of numbers or other information, but you can also use tables invisibly to influence how your page is displayed.  In the early days of html it was common to use a table to create a two column page layout.  We can still do that but now it is **much more acceptable** to use CSS for that purpose.

Here is a complete example that illustrates the use of the following table specific tags

* table  -- This is the main tag for a table
* tr  -- every row in a table starts with a tr tag
* td -- every column in a row is delineated by a ``td`` tag
* th -- You can use the ``th`` tag in place of the ``td`` tag in the first row to make headings


.. activecode:: advhtml_table
   :language: html

    <table width='100%' border=1px cellspacing=0>
    <caption>Table of Scores</caption>
    <tr>
    	<th>Number</th>
    	<th>First Name</th>
    	<th>Last Name</th>
    	<th>Points</th>
    </tr>
    <tr>
    	<td>1</td>
    	<td>Russell</td>
    	<td>Jackson</td>
    	<td>94</td>
    </tr>
    <tr>
    	<td>2</td>
    	<td>John</td>
    	<td>Deere</td>
    	<td>80</td>
    </tr>
    <tr>
    	<td>3</td>
    	<td>Nikola</td>
    	<td>Tesla</td>
    	<td>100</td>
    </tr>
    <tr>
    	<td>4</td>
    	<td>Richard</td>
    	<td>Smith</td>
    	<td>50</td>
    </tr>
    </table>

There are many attributes you can use with the various table tags.

* ``table``
  * width - you can specify a width as a percentage or as a number of pixels.  This attribute is useful for right now, but it's use is not encouraged, as you are better off to use CSS to control the look of your table.  We say that this attribute is **deprecated**
  * border - you can add borders to your tables as in the example above, but this tag is deprecated as well.
  * The spacing between the cells of the table.  Also deprecated.

* ``td``
  * colspan  -- if you have a particular table where you need an extra wide column in some rows you can make a cell of your table span more than one column using the colspan attribute.  Its value is the number of columns.

* ``tr``
  * rowspan -- If you have a particular table where you need an column to span multiple rows you can make a cell of your table span more than one row using the rowspan attribute.  Its value is the number of rows.


Experiment with a table.  What kinds of tags can you include inside each ``td``?  Can you make a table inside another table?

.. Exercise make a two column table with a list in each column

.. Exercise make a table that looks like Name | name then two rows called Telephone with two columns after cell and number followed on the next line by office and the number.  this will combine rowspan and colspan in one project.


Audio
-----

Embedding audio in your webpage allows you to link to various files containing music or speech.  The audio tag looks like the following:

.. code-block:: html

    <audio controls>
        <source src="horse.ogg" type="audio/ogg">
        <source src="horse.mp3" type="audio/mpeg">
        Your browser does not support the audio element.
    </audio>

The ``controls`` attribute provides start/stop/fast-forward/rewind buttons for the listener.  The ``source`` tags inside the ``audio`` tag allow you to provide several different audio formats.  This is because different browsers support different kinds of audio The browser will go through the list, in order, until it finds a format it understands, or else, it will replace the controller with the message at the end.

Video
-----

Embedding video in your webpage allows you to link to various files containing movies.

.. code-block:: html

    <video height=312 width= 540 controls>
        <source src="movie.mp4" type="video/mp4">
        <source src="movie.ogg" type="video/ogg">
        Your browser does not support the video element.
    </video>

The ``controls`` attribute provides start/stop/fast-forward/rewind buttons for the listener.  The ``source`` tags inside the ``video`` tag allow you to provide several different video formats.  This is because different browsers support different kinds of video The browser will go through the list, in order, until it finds a format it understands, or else, it will replace the controller with the message at the end.



IFrames
-------

IFrames allow you to embed a webpage within another webpage.  The activecode examples in this book use an iframe to allow you to experiment with the html, by creating a page within a page.
