Javascript Quiz
===============

For the following question, you may use the textbook or your notes.  You may not google other references.  You have 30 minutes to complete this and you may test it as many times as you need to.

.. qnum::
   :prefix: Q-
   :start: 1


.. timed:: js1timed

   .. mchoice:: q3_5
      :multiple_answers:
      :answer_a: document.body.h1
      :answer_b: document.h1
      :answer_c: document.body
      :answer_d: document.body.style
      :correct: c,d
      :feedback_a: What if there are more than one h1?
      :feedback_b: No, at a minimum the h1 would be inside the body
      :feedback_c: Yes
      :feedback_d: Correct


      Which of the following are legal?


   .. mchoice:: q3_3
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
                  alert(myLi.innerHTML)
              </script>
              </html>

   .. mchoice:: q3_4
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


.. reveal:: jquiz1prog

   1.  Given the following HTML Add a button with a callback function that changes the ``h1`` from "Hello World" to "So Long CS130"  When you change the message you should also arrange it so the color of the text turns blue.  The rest of your page should remain unchanged.

   .. actex:: jsquiz_1
      :language: html

      <html>
      <body>
      <h1 id="hello">Hello World</h1>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
      </body>
      </html>
