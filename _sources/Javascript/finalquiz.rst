Javascript Final Quiz
=====================

For the following questions, you may use the textbook or your notes.  You may not google other references.  You have 30 minutes to complete both parts of the quiz.  Make sure that you complete the
multiple choice questions first, and click "Finish Exam" before you go on to do the coding question.

.. qnum::
   :prefix: Q-
   :start: 1


.. timed:: js2timed

   .. mchoice:: q4_1
      :answer_a: &lt;script&gt;
      :answer_b: &lt;scripting&gt;
      :answer_c: &lt;style&gt;
      :answer_d: &lt;javascript&gt;
      :correct: a
      :feedback_a: Yes
      :feedback_b: close
      :feedback_c: style is for CSS
      :feedback_d: no


      Inside which HTML tag do we put Javascript code?

   .. mchoice:: q4_2
      :answer_a: #demo.innerHTML = "Hello World!";
      :answer_b: document.appendChild("p").innerHTML = "Hello World!";
      :answer_c: document.getElement("p").innerHTML = "Hello World!";
      :answer_d: document.querySelector("#demo").innerHTML = "Hello World!";
      :correct: d
      :feedback_a: No, this is an error
      :feedback_b: No
      :feedback_c: No
      :feedback_d: Yes!

      Which is the correct statement to change the following: ``<p id="demo">This is a demonstration.</p>``

   .. mchoice:: q4_3
      :answer_a: onchange
      :answer_b: onclick
      :answer_c: onmouseover
      :answer_d: onmouseclick
      :correct: b
      :feedback_a: No, this would work only with input elements
      :feedback_b: Yes
      :feedback_c: No, this event does not require a click
      :feedback_d: No, this is not an event

      Which event occurs when the user clicks on an HTML element?


   .. mchoice:: q4_4
      :answer_a: document.body.ol.innerHTML = "&lt;li&gt;"
      :answer_b: myLi = "#newli"
      :answer_c: document.createElement("li")
      :answer_d: myOl.appendChild("li")
      :correct: c
      :feedback_a: No, There is no document.body.ol
      :feedback_b: This just assigns a string to a variable
      :feedback_c: Yes
      :feedback_d: No, appendChild does not create an element

      Which javascript statement correctly creates a new entry for a list?


   .. mchoice:: q4_5
      :answer_a: True
      :answer_b: False
      :correct: b
      :feedback_a: No Feedback
      :feedback_b: No Feedback

      An external JavaScript file must contain the ``<script>`` tag.

   .. mchoice:: q4_6
      :answer_a: msg("Hello World");
      :answer_b: console.log("Hello World");
      :answer_c: alertBox("Hello World");
      :answer_d: alert("Hello World");
      :correct: d
      :feedback_a: No, there is no msg function
      :feedback_b: This adds a message to the javascript console
      :feedback_c: There is no alertBox function
      :feedback_d: Yes!

      How do you write "Hello World" in an alert box?


   .. mchoice:: q4_7
      :answer_a: myFunction = function()
      :answer_b: myFunction()
      :answer_c: function:myFunction()
      :answer_d: &lt;script&gt;function = {}&lt;/script&gt;
      :correct: a
      :feedback_a: Yes
      :feedback_b: No, this calls myFunction
      :feedback_c: No, the : is wrong
      :feedback_d: No, this is syntactically all wrong

      How do you create a function in JavaScript?


   .. mchoice:: q4_8
      :answer_a: myTr.addParent(myRow);
      :answer_b: document.body.innerHTML = "&lt;tr&gt;&lt;tr&gt;&lt;/tr&gt;&lt;/td&gt;"
      :answer_c: myRow.appendChild(myTr);
      :answer_d: myTr.appendChild(myRow);
      :correct: c
      :feedback_a: There is no addParent function
      :feedback_b: No, this changes the entire body
      :feedback_c: Yes
      :feedback_d: No, you have parent and child backward

      Which statement correctly adds a tr element named myTr to the DOM tree?


   .. mchoice:: q4_9
      :answer_a: &lt;script name="xxx.js"&gt;
      :answer_b: &lt;script src="xxx.js"&gt;
      :answer_c: &lt;script href="xxx.js"&gt;
      :answer_d: &lt;link href="xxx.js"&gt;
      :correct: b
      :feedback_a: No, name is mainly used with input tags
      :feedback_b: Yes
      :feedback_c: href is used with the link tag
      :feedback_d: No, link is used for including css

      What is the correct syntax for referring to an external script called "xxx.js"?

   
   .. mchoice:: q4_10
      :answer_a: a1
      :answer_b: a2
      :answer_c: a3
      :answer_d: a5
      :correct: b
      :feedback_a: No, a1 is the grand parent
      :feedback_b: Yes
      :feedback_c: No, a3 is a sibling
      :feedback_d: No, a5 is the child of a4

      Given the following HTML source, what is the parent of the element with the selector "#a4"

      .. code-block:: html

         <body>
         <table id="a1">
         <tr id="a2">
            <td id="a3">Hello</td>
            <td id="a4"><img id="a5" src="hello.jpg"></td>
         </tr>
         </table>
         </body>



Programming Question
--------------------

    Write a function that *each time* it is clicked will do the following:

    1. Turn the background of the page light blue.
    2. Add another H1 to the page that says "So Long 130"
    3. Changes the font color for the H1 to red

    By each time, I mean that if the button is clicked 10 times there should be 10 H1's on the page.


.. activecode:: q4_11
   :language: html

   <html>
   <body>
       <button onclick="finalquiz();">Click Me</button>
       <script type="text/javascript">

       </script>
   </body>
   </html>
