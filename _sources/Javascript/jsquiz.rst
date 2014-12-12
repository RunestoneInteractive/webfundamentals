Javascript Quiz
===============

For the following question, you may use the textbook or your notes.  You may not google other references.  You have 30 minutes to complete this and you may test it as many times as you need to.

1.  Given the following HTML Add a button with a callback function that changes the ``h1`` from "Hello World" to "So Long CS130"  When you change the message you should also arrange it so the color of the text turns blue.  Your final page should still have a button.

.. actex:: jsquiz_1
   :language: html
 
   <html>
   <body>
   <h1 id="hello">Hello World</h1>
   </body>
   </html>


.. qnum:: 
   :prefix: Q-
   :start: 1

Answer the following multiple choice questions.  Make sure to click the check me button to record your answer.  Only your first answer counts.

.. mchoicemf:: q3_2
   :answer_a: Winter Break
   :answer_b: Hello World
   :answer_c: None of the Above
   :correct: a
   :feedback_a: Yes
   :feedback_b: 2 is not greater than 3
   :feedback_c: No, one of the two things is going to happen


   Given the following Javascript snippet, what will the alert box say?

       .. code-block:: javascript
    
           x = 2
           if ( x > 3) {
              alert("hello world")
           } else {
              alert("Winter Break")
           }



.. mchoicemf:: q3_3
   :answer_a: dragon
   :answer_b: wizard
   :answer_c: castle
   :answer_d: dungeon
   :correct: b
   :feedback_a: Not far enough
   :feedback_b: Good Job
   :feedback_c: Not quite, check the order of the ids
   :feedback_d: No, check the ids carefully


   Given the following Javascript snippet, what will the alert box say?

       .. code-block:: html
    
           <html>
           <ul>
              <li id="d">dragon</li>
              <li id="c">wizard</li>
              <li id="b">castle</li>
              <li id="a">dungeon</li>
           </ul>
           <script type="text/javascript">
               myLi = document.querySelector('#c')
               alert(myLi.innerText)
           </script>
           </html>
   
.. mchoicemf:: q3_4
   :answer_a: a string
   :answer_b: the string wizard
   :answer_c: an HTML li element in the tree
   :answer_d: a CSS rule
   :correct: c
   :feedback_a: No, the innerText attribute is a string
   :feedback_b: No, the innerText attribute would be the string wizard
   :feedback_c: Good job
   :feedback_d: Nope, this has nothing to do with CSS yet.


   Referring to the code in the previous question, what kind of thing is ``myLi`` referring to?
