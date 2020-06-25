.. _jsevents:

Javascript Events
=================

Rather than simply list out a host of possible events, let's look at an example that illustrates the use of many events.

Consider the following page:


.. activecode:: js_event_1
   :language: html

    <html>
      <head>
        <title>Colors</title>
      </head>
      <body>
        <label for="redi">Red:</label>
        <input type="text" id="redi" min="0" value="255" /> <br>
        <label for="greeni">Green:</label>
        <input type="text" id="greeni"  value="255" /><br>
        <label for="bluei">Blue:</label>
        <input type="text" id="bluei" value="255" />
        <br>
        <button onclick="changeColor();">Change Color</button>

        <script>
          changeColor = function() {
              red = document.querySelector('#redi').value;
              green = document.querySelector('#greeni').value;
              blue = document.querySelector('#bluei').value;
              colorStr = "rgb("+red+","+green+","+blue+")";
              document.body.style.backgroundColor = colorStr;
          }
        </script>
      </body>
    </html>


Now this first example is similar in many ways to our previous examples, we are using the ``querySelector`` method to obtain a reference to the text input element and reading its value.  The ``onclick`` method on our button attaches the changeColor method to our button.  We call changeColor a callback function, because we set it up now so that it can be called back into service at a later name.  Namely when the button is clicked.

However this is kind of unsatisfying, it would be nice if we could just type a new value into one of the text input boxes and have that cause the color to change.  Another event type that is commonly used with input is the ``onchange`` event.  Let's add an onchange event to the text input elements and attach that to our changeColor function.  Now when you make a change to a color and tap the return key on your keyboard the color will change.  The color will also change if you click outside the text input box.  Give it a try.

.. activecode:: js_event_2
   :language: html

    <html>
      <head>
        <title>Colors</title>
      </head>
      <body>
        <label for="redi">Red:</label>
        <input type="text" id="redi" onchange="changeColor()" value="255" /> <br>
        <label for="greeni">Green:</label>
        <input type="text" id="greeni" onchange="changeColor()" value="255" /><br>
        <label for="bluei">Blue:</label>
        <input type="text" id="bluei" onchange="changeColor()" value="255" />
        <br>
        <button onclick="changeColor();">Change Color</button>

        <script>
          changeColor = function() {
              red = document.querySelector('#redi').value;
              green = document.querySelector('#greeni').value;
              blue = document.querySelector('#bluei').value;
              colorStr = "rgb("+red+","+green+","+blue+")";
              document.body.style.backgroundColor = colorStr;
          }
        </script>
      </body>
    </html>

Typing return or clicking with the mouse is still not as good as we could do.  There are a few other keyboard specific events we can attach to our text input box.  Try changing ``onchange`` attribute in the example above to ``onkeyup``  This event occurs after the user has typed a key and the key has returned to its up position.  In fact there are three events you can experiment with for keyboard keys:

* onkeydown  -- fires when the key is pressed
* onkeypress  -- fires after onkeydown but not for control, shift, alt
* onkeyup -- fires when they key goes up

You may notice some slightly unreliable behavior here.  The problem is that there is a slight timing issue between when the key event happens and when the update to the text input boxes value happens.  It may be that the value is updated before you read it, or it may not be updated until after you read it.  There are ways to work around this, but that would add more difficulty to the example than we want to go into right now.

Now, to explore a few additional events, let's use a nicer user interface element to adjust the color of our background.  Let's use a slider.  We can get a slider by changing the input type to ``range``.

.. activecode:: js_event_3
   :language: html

    <html>
      <head>
        <title>Colors</title>
      </head>
      <body>
        <label for="redi">Red:</label>
        <input type="range" min=0 max=255 id="redi" onchange="changeColor()" value="255" /> <br>
        <label for="greeni">Green:</label>
        <input type="range" min=0 max=255 id="greeni" onchange="changeColor()" value="255" /><br>
        <label for="bluei">Blue:</label>
        <input type="range" min=0 max=255 id="bluei" onchange="changeColor()" value="255" />
        <br>
        <script>
          changeColor = function() {
              red = document.querySelector('#redi').value;
              green = document.querySelector('#greeni').value;
              blue = document.querySelector('#bluei').value;
              colorStr = "rgb(" + red + "," + green + "," + blue + ")";
              document.body.style.backgroundColor = colorStr;
          }
        </script>
      </body>
    </html>

Ok, that is really nice, Now we can move the slider, and whenever we let go, it just updates the color.  But we can go one step further and have the color change as the bar moves!  Change the event from ``onchange`` to ``onmousemove`` to see the results.


Before we leave this section, let's add two more enhancement to this example:

1.  Let's display the values of red, green, and blue
2.  Let's start with a different default value for our rgb colors and have the page automatically change its background color when the page is loaded.

We don't *need* the values to change continuously, so let's update the values when the user stops pressing the mouse key.  To do this we will add a second event attribute to each of our input elements.  The event we need is ``onmouseup``  When we get an onmouseup event we will call another function to display the current values of red, green, and blue.

.. activecode:: js_event_4
   :language: html

    <html>
      <head>
        <title>Colors</title>
      </head>
      <body>
        <label for="redi">Red:</label>
        <input type="range" min=0 max=255 id="redi" onmousemove="changeColor()"
              onmouseup="showValues()" value="125" /> <span id="redv"></span><br>
        <label for="greeni">Green:</label>
        <input type="range" min=0 max=255 id="greeni" onmousemove="changeColor()"
              onmouseup="showValues()" value="125" /><span id="greenv"></span><br>
        <label for="bluei">Blue:</label>
        <input type="range" min=0 max=255 id="bluei" onmousemove="changeColor()"
              onmouseup="showValues()" value="200" /><span id="bluev"></span>

        <br>
        <script>
          changeColor = function() {
              red = document.querySelector('#redi').value;
              green = document.querySelector('#greeni').value;
              blue = document.querySelector('#bluei').value;
              colorStr = "rgb(" + red + "," + green + "," + blue + ")";
              document.body.style.backgroundColor = colorStr;
          }
          showValues = function() {
            document.querySelector('#redv').innerHTML = document.querySelector("#redi").value;
            document.querySelector('#greenv').innerHTML = document.querySelector("#greeni").value;
            document.querySelector('#bluev').innerHTML = document.querySelector("#bluei").value;
          }
          window.onload = function() { changeColor(); showValues(); }
        </script>
      </body>
    </html>


This is a nice polished example now.  So let's take a look at a couple of the new items.  First, we have attached to different events to the input element.  In general you can attach as many events as make sense to an element.  In this case we have one for the mouse movement, and a second for the mouse up.

Second, the showValues function contains an assignment statement that is very compact to write, but may be complicted to follow, so let's look at one of those statements, and then rewrite it in a way that will probably be easier to understand.

.. code-block:: javascript

   document.querySelector('#redv').innerHTML = document.querySelector("#redi").value;

Starting with the right hand side of the assignment statement, the above is getting the value from the slider for the red value.  It is then setting the innerHTML of the ``span`` element that comes after the slider to hold that value.  We could rewrite this statement to be easier to undertand as follows:

.. code-block:: javascript

  theSpan = document.querySelector('#redv');
  theSlider = document.querySelector("#redi");
  sliderVal = theSlider.value;
  theSpan.innerHTML = sliderVal;

The second example breaks up our work into much more manageable chunks:

#.  Get a reference to the span element following the slider.  This is where the value of the slider will be shown.
#.  Get a reference to the input slider node in the document object model.
#. Get the slider value from the value attribute
#. Store the slider value in the innerHTML attribute of the span.

Finally, when the page loads we want to set the background color and have each slider value shown on the page.  To do this we need to attach two functions to the ``window.onload`` event.  This is not possible to do without some fancy Javascript magic, but this illustrates a way of Javascript programming that is fairly common.  Here is the important line:

.. code-block:: javascript

   window.onload = function() { changeColor(); showValues(); }

When the page is fully loaded the ``window.onload`` event happens.  Since we want both of our functions to be called, we create a function (without a name!) to be called, and this function calls both of our functions.  This is a little bit different than how we attach functions to HTML elements, but don't worry about it too much for now.  Just give the example a try to see that it really works just how we want it to.


.. activecode:: js_event_6
   :language: html

   <html>
   <body>
   <button onclick="stop();">Stop</button>
   <script>
     changeColor = function() {
         red = Math.floor(Math.random()*255);
         green = Math.floor(Math.random()*255);
         blue = Math.floor(Math.random()*255);
         colorStr = "rgb(" + red + "," + green + "," + blue + ")";
         document.body.style.backgroundColor = colorStr;
         //window.setInterval(changeColor, 1000);
     }
     stop = function() {
         window.clearInterval(intId);
     }
     intId = window.setInterval(changeColor, 1000);
   </script>
   </body>
   </html>


Events Used in this Section
---------------------------

* onclick
* onchange
* onkeyup
* onkeypress
* onmouseup
* onmousedown
* onmousemove
* window.onload
* window.setInterval
* window.clearInterval

