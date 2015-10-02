Javascript Exercises
====================


#. Make a simple web page that contains an h2 with the word "Hello" and a text input box.  When the user types a word or phrase into the input box, replace the old h2 with the word entered.  Using animation, make the word spin.

  .. actex:: ex_js_4
     :language: html

     <html>
     <style>
     </style>
     <body>
     <h2>Hello</h2>
     </body>
     </html>


#. Make a simple web page that contains a button and a paragraph with the id of ``count`` Whenever this button is pressed increment the count by 1 and update the paragraph text.  Also update the font size so that as the number gets larger, so does the font.

  .. actex:: ex_js_1
     :language: html

     <html>



     </html>


#. Repeat the previous exercise but make a list of numbers.  In this case you will not be able to simply update the innerHTML of the paragraph, you will need to use the ``document.createElement()`` and ``document.appendChild()`` functions to add a new list item.

  .. actex:: ex_js_2
    :language: html

    <html>



    </html>


#. Given the following html.  Every time the button is pressed you should add a row to the table, where the new row of the table contains the sum of the previous two rows.  You should make use  of the lastChild, previousSibling, and innerText attributes in this exercise.

  .. actex:: ex_js_3
     :language: html
     
     <html>
         <body>
            <button onclick="addrow()">Next</button>
            <ul id="mytable"><li id=0>1</li><li id=1>1</li></ul>
         </body>
     </html>
     
