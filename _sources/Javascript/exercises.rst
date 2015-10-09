Javascript Exercises
====================


1. Make a simple web page that contains an h2 with the word "Hello"  a text input box, and a button.  When the user types a word or phrase into the input box and presses the button, replace the old h2 with the word entered.  Using animation, make the word spin.

  .. actex:: ex_js_4
     :language: html

     <html>
     <style>
     </style>
     <body>
     <h2>Hello</h2>
     </body>
     </html>


2. Make a simple web page that contains a button and a paragraph with the id of ``count`` Whenever this button is pressed increment the count by 1 and update the paragraph text.  Also update the font size so that as the number gets larger, so does the font.

  .. actex:: ex_js_1
     :language: html

     <html>



     </html>


3. Repeat the previous exercise but make a list of numbers.  In this case you will not be able to simply update the innerHTML of the paragraph, you will need to use the ``document.createElement()`` and ``document.appendChild()`` functions to add a new list item.

  .. actex:: ex_js_2
    :language: html

    <html>



    </html>


4. Given the following html.  Every time the button is pressed you should add a row to the table, where the new row of the table contains the sum of the previous two rows.  You should make use  of the lastChild, previousSibling, and innerText attributes in this exercise.

  .. actex:: ex_js_3
     :language: html
     
     <html>
         <body>
            <button onclick="addrow()">Next</button>
            <ul id="mytable"><li id=0>1</li><li id=1>1</li></ul>
         </body>
     </html>
     

5. Create an html page with two text input boxes and four buttons.  The buttons should be labeled ``+``, ``-``, ``*``, and ``/``.  When one
   of these buttons is pressed you should get the `value` from both text input boxes and add, subtract, multiply, or divide the
   numbers entered in the text input boxes.  The result should be displayed below the buttons.  **Note** In order to do math
   on the values you read from the text input boxes you will need to use ``Number.parseInt`` on the value.  for example
   suppose you get a reference to input box 1 using ``myIn1 = document.querySelector("#in1id");`` then the statement ``value1 = Number.parseInt(myIn1.value)`` converts the string from the text input box to an integer.  In fact
   most of the time Javascript will do the conversion for you automatically except for addition.

  .. actex:: ex_js_5
    :language: html

    <html>



    </html>


6.  Starting with the code given, create a page that looks like the following image:  The rest of the page must be created
    using javascript.  You must use ``document.createElement`` and the ``appendChild`` functions.

    .. image:: Figures/cePage.png
       :width: 350px

    .. actex:: ex_js_6
       :language: html

       <html>
       <body>
       <button onclick="makePage();">Click Here</button>
       </body>

       </html>
