Template Engines
================

.. Writing about templates is a challenge because we are running the result of rst through a template system
.. One hack is to paste a zero width space between https://codepen.io/chriscoyier/pen/iLKwm

There are many benefits to using templates.

* Separation of the view from the controller and model code.
* Increased productivity.
* Ease of creating a site with a unified design.
* Division of labor.  Designers can now work on template files using html plus a bit more without needing to know how to write Python.

At the simplest level templates are not much different than a Python formatted string.  However they are much more convenient to use, and have many more features that we will explore shortly.  Here is a simple example:

.. code-block:: python

   from jinja2 import Template
   template = Template('Hello {​{ name }}!')
   template.render(name='John Doe')

A slightly more complicated example goes like this:

.. code-block:: python

   from jinja2 import Environment, FileSystemLoader
   env = Environment(loader=FileSystemLoader('/path/to/templates))
   t = env.get_template('foo.html')
   t.render(name='Luther')

This example shows how we can set up an environment that can be shared among many functions.  This environment takes care of the details behind locating and reading our templates from a file when we want to use them.  The foo.html file could look like this:

.. code-block:: html

   <html>
       <body>
       <h1>Hello {​{ name }}</h1>
       </body>
   </html>

The values inside the double curlies are not limited to being string objects, although they must have an ``__str__`` method if they are going to be useful.  Consider an instance of a Student class that has instance variables for firstname, lastname, and gpa.  Let's change our template to look like the following:

.. code-block:: html

   <html>
       <body>
           <h1>Hello {​{ s.firstname }} {​{ s.lastname }}</h1>
           <p>Your gpa is {​{ s.gpa }}.</p>
       </body>
   </html>


Assuming we have a student object called joe we can render the template above with the line:  ``t.render(s=joe)``  This would also work if joe was a dictionary and had keys firstname, lastname, and gpa.  The dot notation works for either attributes or items in a dictionary  (``__getattr__`` or ``__getitem__``) for those of you who like magic method speak.


Loops in Templates
------------------

Let's suppose you want to make a table in a template.  The ideal would be to pass render a list of things, and have the template turn the list into a table.  (or an unordered list or whatever)  This is easy to do.

.. code-block:: html

   <html>
       <body>
           <h1>The first {​{ plist|length }} prime numbers</h1>
           <table>
               {% for i in plist: %}
                   <tr><td>{​{ i }}</td></tr>
               {% endfor %}
           </table>
       </body>
   </html>


This introduces several interesting new features of templates.

1.  The ``{% ... %}`` notation is used to include a non-rendering bit of code in the template.  In this example we introduce a for loop.  Notice that since html does not require you to indent things we need an endfor to delimit the end of the for loop.

2.  Jinja2 includes a huge number of filters that you can use on a variable.  The filter ``plist|length`` will render as the number of elements in the plist list.


Conditionals in Templates
-------------------------

In addition to loops you can also have a conditional in a template for example:

.. code-block:: html

   <html>
       <body>
           {% if name %}
           <h1>Hello {​{ name }} </h1>
           {% else %}
           <h1>Hello World</h1>
           {% endif %}
       </body>
   </html>


Template Inheritance
--------------------

The real power of templates comes when you use template inheritance.  The following scenario is very common:

1.  base.html  - This file contains the layout that will be used throughout the site, along with all of the links to css files and includes of javascript.  The base.html file will define a set of blocks that have default content, but can be overridden by other templates.
1.  index.html --  The landing page, that inherits from base.html and customizes some blocks for the main page.
1.  other child pages, will also inherit from base.html annd make their own customizations.

For example let's suppose you have a base.html file that looks like this:

.. code-block:: html

   <html>
   <head>
       {% block head %}
       <link rel="stylesheet" href="static/style.css" />
       <title>{% block title %}{% endblock %} - My Webpage</title>
       {% endblock %}
   </head>
   <body>
       <main>{% block content %}{% endblock %}</main>
       <footer>
           {% block footer %}
           Creative Commons 2014 by <a href="http://domain.invalid/">you</a>.
           {% endblock %}
       </footer>
   </body>


Running this through the Jinja2 renderer gives us this:

.. code-block:: html

   <html>
   <head>

      <link rel="stylesheet" href="static/style.css" />
      <title> - My Webpage</title>

   </head>
   <body>
      <main></main>
      <footer>

          Creative Commons 2014 by <a href="http://domain.invalid/">you</a>.

      </footer>
   </body>


Now let's create a child template that contains a title and some real content.

.. code-block:: html

   .. code-block:: html

      {% block content %}
      <h1>Tempates are awesome for 10 reasons</h1>
      <ol>
          {% for i in reasons: %}
          <li>Reason {​{ i }}</li>
          {% endfor %}
      </ol>
      {% endblock %}



And render it with ``render(reasons=[1,2,3,4,5])``

.. code-block:: html

   <html>
   <head>

      <link rel="stylesheet" href="static/style.css" />
      <title>
   Great Title
    - My Webpage</title>

   </head>
   <body>
      <main>
   <h1>Tempates are awesome for 5 reasons</h1>
   <ol>

       <li>Reason 1</li>

       <li>Reason 2</li>

       <li>Reason 3</li>

       <li>Reason 4</li>

       <li>Reason 5</li>

   </ol>
   </main>
      <footer>

          Creative Commons 2014 by <a href="http://domain.invalid/">you</a>.

      </footer>
   </body>


Notice that the header and footer are intact, however the child has the title "Great Title"  and the content of the child has been inserted into the content block.


Templates in Flask
------------------

To use Jinja templates in flask is easy.

1.  You need to make a templates subdirectory in your main project directory.
2.  Add ``from flask import render_template`` to your Python.
3.  Then from one of your controller functions, rather than returning a big string, you simple invoke the ``render_template`` function:  ``return render_template('todo.html',todolist=todolist))``

Remember that in flask our controller functions return an iterable.  The render_template function returns such an interable.  It's just a string, so you can call the render_template function and print the results if you like.
