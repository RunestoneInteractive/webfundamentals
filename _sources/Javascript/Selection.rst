Selection
=========

Selection allows us to ask questions, and take different actions depending on the answers.  We use selection every day as we go about our duties.  If its cold out we put on some extra clothes.  If its raining we grab our umbrella before we leave the house.  These are examples of the kinds of decisions we make.  More formally we can put this into an ``if`` statement.  ``if`` it is raining, ``then`` we take our umbrella.

Javascript allows us to ask questions like this  using an ``if`` statement as well.  An if statement is often used in Javascript to check an input value from
a text box to make sure that it is a good value.  For example if colors can only be in the range from 0 to 255 we could check the value of an input box as follows:


.. activecode:: select_1
   :language: html
   
   <html>
      <label for="red">Red:</label>
      <input id="red" type="text" onchange="checkme()" />
      <script type="text/javascript">
      checkme = function() {
         textbox = document.querySelector("#red")
         if (textbox.value > 255) {
            alert("Value is too large, must be less than 256")
         }
      }
      </script>
   </html>

