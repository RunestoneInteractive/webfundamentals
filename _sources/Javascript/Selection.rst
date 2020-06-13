Selection
=========

Selection allows us to ask questions, and take different actions depending on the answers.  We use selection every day as we go about our duties.  If it's cold out we put on some extra clothes.  If it's raining we grab our umbrella before we leave the house.  These are examples of the kinds of decisions we make.  More formally we can put this into an ``if`` statement.  ``if`` it is raining, ``then`` we take our umbrella.

Javascript allows us to ask questions like this  using an ``if`` statement as well.  An if statement is often used in Javascript to check an input value from
a text box to make sure that it is a good value.  For example if colors can only be in the range from 0 to 255 we could check the value of an input box as follows:


.. activecode:: select_1
   :language: html
   
   <html>
      <label for="red">Red:</label>
      <input id="red" type="text" onchange="checkme(this)" />
      <label for="green">Green:</label>
      <input id="green" type="text" onchange="checkme(this)" />
      <label for="blue">Blue:</label>
      <input id="blue" type="text" onchange="checkme(this)" />

      <script type="text/javascript">
      checkme = function(textbox) {
         if (textbox.value > 255) {
            alert("Value is too large, must be less than 256");
            textbox.value = 255;
         }
      }
      </script>
   </html>


In this example we have one function that can check the values for any of our color text input boxes.  Once again we have the interesting issue of how does the checkme function know which text box it is supposed to check?  When we are setting up a call from html we can pass ``this`` as a special parameter that refers to the object that the onchange is connected to.


If  you want to get a little practice, add another if statement to ``checkme`` that ensures the value entered by the user is greater than or equal to zero.


Guessing Game
=============

Here is a simple application that uses selection to allow you play the old guessing game.

The computer will select a number between 1 and 100.  You can type in your guess into the box and the computer will tell you when you are right, or if your guess is too high or too low.

To select our number we will use another of Javascripts builting facilities to make up a random number.  This is called ``Math.random()``  It generates a random number between 0 and 1, so we'll have to do a little bit of work to turn that into a random number between 1 and 100.


.. activecode:: select_2
   :language: html

   <html>
   
   <body>   
      <label for="red">Guess:</label>
      <input id="guess" type="text" />
      <button onclick="check()">Check</button>
      <script type="text/javascript">
      theNumber = Math.floor(Math.random()*100)
      check = function() {
          guess = document.querySelector("#guess").value;
          if (guess == theNumber) {
              alert("you are right!")
          } else {
              if (guess < theNumber) {
                  alert("you are too low")
              } else {
                  alert("you are too high")
              }
          }
      }
      </script>
   </body>
   </html>
   
Things to do:

* Change this to not use an alert.  Update the innerHTML of a paragraph to tell the user if they are too high or too low.
* Add a dynamically created list to keep track of the guesses, color the guesses that are too high red, and the guesses that are too low blow.
* Keep track of the number of guesses and tell the user at the end how many guesses they needed.
* To play a new game, you must now reload the page.  Can you add a reset button that makes up a new number and clears out everything else?

