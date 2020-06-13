The Javascript Programming Language
===================================

We have made excellent progress toward learning about Web Programming.  You have learned something about two of the three primary web programming languages.  We will continue to explore HTML and CSS in more detail, but it is now time to turn our attention to Javascript.

Although we have been calling HTML and CSS programming languages, they do not have nearly the power of Javascript.  Once you learn Javascript you could can write any program that could be written.

Javascript is a procedural language.  With HTML and especially CSS the order of things is not always important, but with Javascript, the order that you do things in is very important.  Javascript is also called an **object oriented** language.  That means that we will be working with objects in our imaginary world of the browser.  Objects can tell us things we want to know, and objects know how to do many things.  We only need to write a javascript program to ask or tell.

But, let's not get caught up in a bunch of formal talk about computer science and programming language theory, let's start with a simple example of one of the things that Javascript is good at doing, namely making buttons do interesting things.  For our first program let's make a button that changes the background color of our window.

.. activecode:: js_first
   :language: html
   
   <html>
      <body>
         <h1>Hello World!!</h1>
         <button onclick="changeThisPageFunc();">Click Me!</button>
         <script type="text/javascript">
            changeThisPageFunc = function() {
               document.body.style.backgroundColor = "lightblue";
               document.body.innerHTML = "<h1>I am a little blue today</h1>";
            }
         </script>
      </body>
   </html>
   
Now that example may look very complex to you, and in fact it does demonstrate **LOTS** of important aspects of programming.  But do not worry, we'll dissect this example carefully so that you fully understand what is going on.

Here are some questions that we should answer about the example above:

#. Button?  We haven't talked about a ``button`` tag before, whats the deal with that?
#. What is the ``onclick`` attribute for?
#. script tag?  Again this is a new one why a ``script`` tag?
#. What in the world does all of that stuff inside the script tag mean?
#. What happened to my button!?!

Those are all very good questions, I'm glad you asked.  Let's take them one at a time right now, and then we'll expand upon the ideas in the next few sections.

The button tag is part of HTML that is going to allow us to make interactive websites.  In addition to buttons there are other things like check boxes, and text input, that we will talk about in the next section.  For now we will use the button as a simple example, of something we are all used to using every day.

The ``onclick`` attribute is the way we answer the question, "what should this button do when someone clicks on it."  The answer in this case is may lead to confusion, but hopefully you at least get the idea that when the button is clicked we want to "change this page".  The way we are going to do this is through a **function call**. You have used functions in math class many times, and these are not all that different.  The important thing to remember is that functions are **abstractions** of things that need doing.  We all use abstractions all the time in our everyday life.  

For example, you may tell your friend, "I'm going to Computer Science now." this is an abstraction of the following hypothetical steps:

#.  Get out of bed.
#.  Get dressed
#.  Walk out of your room, down the hall and wait for the elevator.
#.  Take the elevator to the fourth floor.
#.  Walk out of the elevator, out of the door, and across campus to Olin hall.
#.  Go in the door, and up the stairs to second floor, enter room 202 and find your favorite place to sit.

That would be a long boring conversation if you responded with all 6 of those steps every time a friend asked you what you were doing. But your friend understands those steps are necessary when you say you are going to class.   Further more even step 1 is an abstraction of several smaller steps:  Sit up, remove the covers, slide my legs over the side of the bed, stand up (or climb down the ladder).  

This brings us to the next question, the ``script`` tag is one way that we can include Javascript in our HTML.  But like CSS we will see that we can, and should, also include Javascript by putting it in its own file and including it.  More on that later.

The stuff inside the script tag is Javascript code. This code contains a **function definition** which is how we create our very own abstractions. Unlike your friend to naturally understands what it means to go to class, computers are very dumb, and very literal, they only do what you tell them.  In this case there are two steps to our abstraction.  One changes the background color of the body, and the second one changes our message.  These lines are also abstractions of a very complicated set of steps that we as programmers don't need to know the details of right now.  We just need to know which abstractions the browser understands.

Let's defer the question of what happened to the button for just a bit.  In the meantime experiment with the Javascript code by trying the following things:

#. Make the background light green
#. Experiment with different style elements we have learned about through CSS.  See if you can add a line that makes the text red.  
#. Can you change the fontSize to 48pt?
#. What does that tell you about ``document.body.style``?
#. Change the wording inside the ``<h1>`` tag in the Javascript.
#. What happens if you add ``<button>Click Me</button>`` after the closing ``</h1>``?


Let's look at a little different example that accomplishes the same thing, but illustrates how CSS, Javascript, and HTML all work together.
In this example rather than setting the color of the background directly, we will make the body have the class attribute "myclass" when the button is clicked.

Now, 

.. activecode:: js_second
   :language: html
   
   <html>
      <head>
         <style>
         .myclass {
            background-color: lightblue;
         }
         </style>
      </head>
      <body>
         <h1>Hello World!!</h1>
         
         <button onclick="changeThisPageFunc();">Click Me!</button>
         <script type="text/javascript">
            changeThisPageFunc = function() {
               alert("body has class = "+document.body.className);
               document.body.className = "myclass";
               alert("body has class = "+document.body.className);
               document.body.innerHTML = "<h1>I am a little blue today</h1>";
            }
         </script>
      </body>
   </html>
