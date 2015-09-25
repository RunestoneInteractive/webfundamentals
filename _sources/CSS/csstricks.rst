CSS Tricks
==========

**DRAFT**  This chapter is a work in progress.

CSS is used for all kinds of special effects that make web pages look good.  In this section we will investigate some
of them.

Hover
-----

.. activecode:: hover1
   :language: html

    <html>
        <head>
            <title>Home</title>
            <style>
            header {
                position: fixed;
                background-color: #bbbbbb;
                top: 0px;
                left: 0px;
                width: 100%;
                height: 20px;
            }
            nav {
                margin-top: 20px;
                margin-bottom: 0px;
                background-color: green;
            }
            nav li {
               display: inline;
            }

            nav li:hover {
               background-color: lightblue;
            }
            section {
                float: left;
                width: 20%;
                height: 500px;
                background-color: blue;
                color: white;
            }
            aside {
                float: left;
                width: 80%;
                height: 500px;
                background-color: red;
            }
            footer {
                clear: both;
                background-color: yellow;
            }
            body {
                background-color: black;
                margin: 0px;
            }
            </style>

        </head>
        <body>
            <header>
                A header that stays stuck to the top.
            </header>
            <nav>
                <ul>
                <li>About</li>
                <li>Papers</li>
                <li>Donate</li>
                </ul>
            </nav>
            <section>
                This would be a good place for a table of contents
            </section>
            <aside>
                This is the main content area
                <img src="http://interactivepython.org/runestone/static/webfundamentals/_images/img_sem_elements.gif" />
            </aside>
            <footer>
                Copyright Area, Contact Us.
            </footer>
        </body>
    </html>


* Add link with a :hover pseudo-class to the example above.
* Add an ``h2`` with the title more info.  Underneath the h2 add  a ``main`` container with a paragraph.  The details element should be initially hidden and only appear when you hover the cursor over the h2.  Hint:  the ``~`` character allows you to write a selector that matches a sibling.

Animation
---------

Using the ``@keyframes`` keyword we can create an animation and then apply that animation to other css elements.  Check out the following example
that animates the background color.  With keyframes we can specify a starting and and ending condition using
``from`` and ``to`` or we can specify multiple points along the animation using ``xx%``.

Animation should work as shown in all modern browsers.  Safari version 8 and earlier will require the ``-webkit-`` prefix to be added.


.. activecode:: animation1
   :language: html

   <html>
   <head>
     <style>
     @keyframes example {
            from {background-color: red;}
            to {background-color: yellow;}
     }

     div {
         width: 100px;
         height: 100px;
         background-color: red;
         animation-name: example;
         animation-duration: 4s;
     }
     </style>
   </head>
   <body>
   <div>
   <h1>Hello World</h1>
   </div>
   </body>
   </html>


Experiment with the following:

* ``animation-delay: 2s;``
* ``animation-iteration-count: infinite;``
* ``animation-direction: alternate;``

.. code-block:: css

    @keyframes spin {
        from {
            transform: rotate(0deg);
        } to {
            transform: rotate(360deg);
        }
    }


.. code-block:: css

   @keyframes moveit {
       from {
           top: 0px;
           left: 0px;
       }
       to {
           top: 300px;
           left: 300px;
       }
   }

* Add an image to the picture and make it spin infinitely.
* try creating a scale animation

