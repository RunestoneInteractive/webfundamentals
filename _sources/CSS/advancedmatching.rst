The Dropdown Menu Project
=========================

In this section we will take on a full project to make some nice navigational dropdown menus with submenus.  This is not a simple project, so we will follow good programming practice and develop our solution iteratively.

Step One
--------

Before we add any CSS rules at all let's get the menu structure and some page contents in place.   This is not going to look pretty but it will give us a starting place.  This  is almost always a good practice in web development.  Get the basic structure in place first, then incrementally make some improvements.  The reason to do it this way is simple, if you add small things one at a time, it's easy to tell when you do something wrong, and you automatically know that it was the last thing you did that caused the problem.

We have two main semantic areas in our page, the navigation menu main contents.  We will separate these two by placing the navigation menu inside a nav tag, and the main contents inside a main tag.

.. activecode:: menu_1
   :language: html

   <html>
   <head>
   <title>SubMenus</title>
   <style type='text/css'>

   </style>
   </head>
   <body>

   <h1>Fundamentals of Web Programming</h1>

   <nav>
   <ul >
    <li><a href='/'>Home</a></li>
    <li><a href='#'>Syllabus</a>
     <ul>
      <li><a href='#'>Text Book</a></li>
      <li><a href='#'>Office Hours</a></li>
      <li><a href='#'>Grading Policy</a></li>
      <li><a href='#'>Learning Goals</a></li>
     </ul>
    </li>
    <li><a href='#'>Resources</a></li>
    <li><a href='#'>Publications</a>
     <ul>
      <li><a href='#'>Articles</a></li>
      <li><a href='#'>Tutorials</a>
       <ul>
        <li><a href='#'>HTML</a></li>
        <li><a href='#'>CSS</a></li>
        <li><a href='#'>SVG</a></li>
        <li><a href='#'>XML</a></li>
       </ul>
      </li>
      <li><a href='#'>Assignments</a></li>
     </ul>
    </li>
    <li><a href='#'>Contact</a></li>
   </ul>
   </nav>

   <main>
   <p>
   Lorem ipsum, dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.
    Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse molestie consequat, vel illum dolore eu feugiat nulla facilisis at vero eros et accumsan et iusto odio dignissim qui blandit praesent luptatum zzril delenit augue duis dolore te feugait nulla facilisi.
   Lorem ipsum, dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat. Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse molestie consequat, vel illum dolore eu feugiat nulla facilisis at vero eros et accumsan et iusto odio dignissim qui blandit praesent luptatum zzril delenit augue duis dolore te feugait nulla facilisi.
   Lorem ipsum, dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.
   </p>
   </main>
   </body>
   </html>



Step Two
--------

Now that the content is in place, let us set some background colors for things, and position our semantic elements.  In this case we want our navigational menu to be on the left side of the page, with the main content to the right.

We can position on nav on the left and have the main just to the right of it using the ``float: left`` property.  Notice that we set our width for the nav element to be ``7em``, using an ``em`` as a unit of measure in this case is a good idea because it will scale the width of our nav bar if we change the size of our font.  Try setting the font size in the body tag and notice that everything grows proportionally.

We give the nav its own background color for now, just to make it easy to differentiate between area that belongs to the nav, and the area that belongs to main.

.. activecode:: menu_2
   :language: html

   <html>
   <head>
   <title>SubMenus</title>
   <style type='text/css'>
   body {
       background: #EEE;
       color: #000;
   }

   h1 {
       color: #AAA;
       border-bottom: 1px solid;
       margin-bottom: 0;
   }

   main {
       color: #CCC;
       margin-left: 7em;
       padding: 1px 0 1px 5%;
       border-left: 1px solid;
   }

   nav {
       float: left;
       width: 7em;
       background: #FDD;
   }
   </style>
   </head>
   <body>

   <h1>Fundamentals of Web Programming</h1>

   <nav>
   <ul>
    <li><a href='/'>Home</a></li>
    <li><a href='#'>Syllabus</a>
     <ul>
      <li><a href='#'>Text Book</a></li>
      <li><a href='#'>Office Hours</a></li>
      <li><a href='#'>Grading Policy</a></li>
      <li><a href='#'>Learning Goals</a></li>
     </ul>
    </li>
    <li><a href='#'>Resources</a></li>
    <li><a href='#'>Publications</a>
     <ul>
      <li><a href='#'>Articles</a></li>
      <li><a href='#'>Tutorials</a>
       <ul>
        <li><a href='#'>HTML</a></li>
        <li><a href='#'>CSS</a></li>
        <li><a href='#'>SVG</a></li>
        <li><a href='#'>XML</a></li>
       </ul>
      </li>
      <li><a href='#'>Assignments</a></li>
     </ul>
    </li>
    <li><a href='#'>Contact</a></li>
   </ul>
   </nav>

   <main>
   <p>
   Lorem ipsum, dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.
    Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse molestie consequat, vel illum dolore eu feugiat nulla facilisis at vero eros et accumsan et iusto odio dignissim qui blandit praesent luptatum zzril delenit augue duis dolore te feugait nulla facilisi.
   Lorem ipsum, dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat. Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse molestie consequat, vel illum dolore eu feugiat nulla facilisis at vero eros et accumsan et iusto odio dignissim qui blandit praesent luptatum zzril delenit augue duis dolore te feugait nulla facilisi.
   Lorem ipsum, dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.

   </p>
   </main>
   </body>
   </html>


Step Three
----------

Next let's change our indentation of the sublists using the following three rules:

.. code-block:: css

   nav ul {
        margin: 0;
        padding: 0;
        width: 7em;
        background: white;
        border: 1px solid;
   }

   nav li {
        position: relative;
        list-style: none;
        margin: 0;
        border-bottom: 1px solid #CCC;
   }

   nav ul ul {
       position: absolute;
       top: 0;
       left: 7em;
       display: block;
   }

We set the margin of the uls inside the the nav element (nav ul) to have a margin of 0 because by default they have a non-zero margin, which will make our positioning more difficult later.  The same goes for the padding.  We also set the background to white, and give the bottom a little border.  Setting the list sytle to none removes the bullets.

Notice that we add two position properties.  The ``nav li`` items are positioned relatively, but we don't change the top or left property.  This is simply in preparation for the next rule  ``nav ul ul`` which positions the submenus using absolute measurements.  We can use absolute here because the ul's in question will all be children of li's that have been positioned relatively.  Remember the rule for using absolute position is that the absolute position is relative to the first container that is not statically positioned.  Or else the html tag if no non static tag is found.

.. activecode:: menu_3
   :language: html

   <html>
   <head>
   <title>SubMenus</title>
   <style type='text/css'>
   body {
       background: #EEE;
       color: #000;
   }

   h1 {
       color: #AAA;
       border-bottom: 1px solid;
       margin-bottom: 0;
   }

   main {
       color: #CCC;
       margin-left: 7em;
       padding: 1px 0 1px 5%;
       border-left: 1px solid;
   }

   nav {
       float: left;
       width: 7em;
       background: #FDD;
   }

   nav ul {
        margin: 0;
        padding: 0;
        width: 7em;
        background: white;
        border: 1px solid;
   }

   nav li {
        position: relative;
        list-style: none;
        margin: 0;
        border-bottom: 1px solid #CCC;
   }

   nav ul ul {
       position: absolute;
       top: 0;
       left: 7em;
       display: block;
   }

   </style>
   </head>
   <body>

   <h1>Fundamentals of Web Programming</h1>

   <nav>
   <ul >
    <li><a href='/'>Home</a></li>
    <li><a href='#'>Syllabus</a>
     <ul>
      <li><a href='#'>Text Book</a></li>
      <li><a href='#'>Office Hours</a></li>
      <li><a href='#'>Grading Policy</a></li>
      <li><a href='#'>Learning Goals</a></li>
     </ul>
    </li>
    <li><a href='#'>Resources</a></li>
    <li><a href='#'>Publications</a>
     <ul>
      <li><a href='#'>Articles</a></li>
      <li><a href='#'>Tutorials</a>
       <ul>
        <li><a href='#'>HTML</a></li>
        <li><a href='#'>CSS</a></li>
        <li><a href='#'>SVG</a></li>
        <li><a href='#'>XML</a></li>
       </ul>
      </li>
      <li><a href='#'>Assignments</a></li>
     </ul>
    </li>
    <li><a href='#'>Contact</a></li>
   </ul>
   </nav>

   <main>
   <p>
   Lorem ipsum, dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.
    Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse molestie consequat, vel illum dolore eu feugiat nulla facilisis at vero eros et accumsan et iusto odio dignissim qui blandit praesent luptatum zzril delenit augue duis dolore te feugait nulla facilisi.
   Lorem ipsum, dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat. Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse molestie consequat, vel illum dolore eu feugiat nulla facilisis at vero eros et accumsan et iusto odio dignissim qui blandit praesent luptatum zzril delenit augue duis dolore te feugait nulla facilisi.
   Lorem ipsum, dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.

   </p>

   </main>

   </body>
   </html>


Step Four
---------

In this step we add single rule to deal with a small problem.  The problem is that you can only click on a link when the mouse is hovering over a link.  We want to be able to click anywhere in the box containing an a tag.  Changing the display property of the a tag will allow it to fill the enclosing container

.. code-block:: css

   nav li a {
       display: block;
       padding: 0.25em 0 0.25em 0.5em;
       text-decoration: none;
   }


.. activecode:: menu_4
   :language: html

   <html>
   <head>
   <title>SubMenus</title>
   <style type='text/css'>
   body {
       background: #EEE;
       color: #000;
   }

   h1 {
       color: #AAA;
       border-bottom: 1px solid;
       margin-bottom: 0;
   }

   main {
       color: #CCC;
       margin-left: 7em;
       padding: 1px 0 1px 5%;
       border-left: 1px solid;
   }

   nav {
       float: left;
       width: 7em;
       background: #FDD;
   }

   nav ul {
        margin: 0;
        padding: 0;
        width: 7em;
        background: white;
        border: 1px solid;
   }

   nav li {
        position: relative;
        list-style: none;
        margin: 0;
        border-bottom: 1px solid #CCC;
   }

   nav ul ul {
       position: absolute;
       top: 0;
       left: 7em;
       display: block;
   }

   nav li a {
       display: block;
       padding: 0.25em 0 0.25em 0.5em;
       text-decoration: none;
   }

   </style>
   </head>
   <body>

   <h1>Fundamentals of Web Programming</h1>

   <nav>
   <ul class='level1'>
    <li><a href='/'>Home</a></li>
    <li class='submenu'><a href='#'>Syllabus</a>
     <ul class='level2'>
      <li><a href='#'>Text Book</a></li>
      <li><a href='#'>Office Hours</a></li>
      <li><a href='#'>Grading Policy</a></li>
      <li><a href='#'>Learning Goals</a></li>
     </ul>
    </li>
    <li><a href='#'>Resources</a></li>
    <li class='submenu'><a href='#'>Publications</a>
     <ul class='level2'>
      <li><a href='#'>Articles</a></li>
      <li class='submenu'><a href='#'>Tutorials</a>
       <ul class='level3'>
        <li><a href='#'>HTML</a></li>
        <li><a href='#'>CSS</a></li>
        <li><a href='#'>SVG</a></li>
        <li><a href='#'>XML</a></li>
       </ul>
      </li>
      <li><a href='#'>Assignments</a></li>
     </ul>
    </li>
    <li><a href='#'>Contact</a></li>
   </ul>
   </nav>

   <main>
   <p>
   Lorem ipsum, dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.
    Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse molestie consequat, vel illum dolore eu feugiat nulla facilisis at vero eros et accumsan et iusto odio dignissim qui blandit praesent luptatum zzril delenit augue duis dolore te feugait nulla facilisi.
   Lorem ipsum, dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat. Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse molestie consequat, vel illum dolore eu feugiat nulla facilisis at vero eros et accumsan et iusto odio dignissim qui blandit praesent luptatum zzril delenit augue duis dolore te feugait nulla facilisi.
   Lorem ipsum, dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.

   </p>

   </main>

   </body>
   </html>


Step Five
---------

Before moving on to the final set of new rules, modify the code above and just change the display property in the ``nav ul ul`` rule to none;  When you redisplay our page you will see that this makes all the submenus invisible.  I've made this change to that rule in the next step, but it's good to see how it works all by itself.

Finally we will bring everything together, with a few small rules.

Let's change the background color when we hover over any list item.

Let's also add a background image to indicate that something is a submenu.

The last rule makes a submenu visible!  ``display: block;``  But we want to distinguish between the various levels by adding classes to them.  So we need to also modify our html to add classes to the ul's and the li's.

.. code-block:: css

   nav li:hover {
       background: #EBB;
   }

   nav li.submenu {
       background: url(http://...submenu.gif) 95% 50% no-repeat;
   }

   nav li.submenu:hover {
       background-color: #EDD;
   }

   nav ul.level1 li.submenu:hover ul.level2,
   nav ul.level2 li.submenu:hover ul.level3 {
       display:block;
   }

The change we need to make is to

.. activecode:: menu_5
   :language: html

   <html>
   <head>
   <title>SubMenus</title>
   <style type='text/css'>
   body {
       background: #EEEEEE;
       color: #000000;
   }

   h1 {
       color: #AAA;
       border-bottom: 1px solid;
       margin-bottom: 0;
   }

   main {
       color: #CCC;
       margin-left: 7em;
       padding: 1px 0 1px 5%;
       border-left: 1px solid;
   }

   nav {
       float: left;
       width: 7em;
       background: #FDD;
   }

   nav ul {
        margin: 0;
        padding: 0;
        width: 7em;
        background: white;
        border: 1px solid;
   }

   nav li {
        position: relative;
        list-style: none;
        margin: 0;
        border-bottom: 1px solid #CCC;
   }

   nav ul ul {
       position: absolute;
       top: 0;
       left: 7em;
       display: none;
   }

   nav li a {
       display: block;
       padding: 0.25em 0 0.25em 0.5em;
       text-decoration: none;
   }

   nav li:hover {
       background: #6F99F2;
   }

   nav li.submenu {
       background: url(http://interactivepython.org/runestone/static/webfundamentals/_static/submenu.gif) 95% 50% no-repeat;
   }

   nav li.submenu:hover {
       background-color: #EDD;
   }



   nav ul.level1 li.submenu:hover ul.level2,
   nav ul.level2 li.submenu:hover ul.level3 {
       display:block;
   }
   </style>
   </head>
   <body>

   <h1>Fundamentals of Web Programming</h1>

   <nav>
   <ul class='level1'>
    <li><a href='/'>Home</a></li>
    <li class='submenu'><a href='#'>Syllabus</a>
     <ul class='level2'>
      <li><a href='#'>Text Book</a></li>
      <li><a href='#'>Office Hours</a></li>
      <li><a href='#'>Grading Policy</a></li>
      <li><a href='#'>Learning Goals</a></li>
     </ul>
    </li>
    <li><a href='#'>Resources</a></li>
    <li class='submenu'><a href='#'>Publications</a>
     <ul class='level2'>
      <li><a href='#'>Articles</a></li>
      <li class='submenu'><a href='#'>Tutorials</a>
       <ul class='level3'>
        <li><a href='#'>HTML</a></li>
        <li><a href='#'>CSS</a></li>
        <li><a href='#'>SVG</a></li>
        <li><a href='#'>XML</a></li>
       </ul>
      </li>
      <li><a href='#'>Assignments</a></li>
     </ul>
    </li>
    <li><a href='#'>Contact</a></li>
   </ul>
   </nav>

   <main>
   <p>
   Lorem ipsum, dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.
    Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse molestie consequat, vel illum dolore eu feugiat nulla facilisis at vero eros et accumsan et iusto odio dignissim qui blandit praesent luptatum zzril delenit augue duis dolore te feugait nulla facilisi.
   Lorem ipsum, dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat. Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse molestie consequat, vel illum dolore eu feugiat nulla facilisis at vero eros et accumsan et iusto odio dignissim qui blandit praesent luptatum zzril delenit augue duis dolore te feugait nulla facilisi.
   Lorem ipsum, dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.

   </p>

   </main>

   </body>
   </html>

