Template Engines
================

There are many benefits to using templates.  

* Separation of the view from the controller and model code.
* Increased productivity.
* Ease of creating a site with a unified design.
* Division of labor.  Designers can now work on template files using html plus a bit more without needing to know how to write Python.

At the simplest level templates are not much different than a Python formatted string.  However they are much more convenient to use, and have many more features that we will explore shortly.  Here is a simple example:

.. code-block:: python

   from jinja2 import Template
   template = Template('Hello {{ name }}!')
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
       <h1>Hello {{ name }}</h1>
       </body>
   </html>

The values inside the double curlies are not limited to being string objects, although they must have an ``__str__`` method if they are going to be useful.  Consider an instance of a Student class that has instance variables for firstname, lastname, and gpa.  Lets change our template to look like the following:

.. code-block:: html

   <html>
       <body>
           <h1>Hello {{ s.firstname }} {{ s.lastname }}</h1>
           <p>Your gpa is {{ s.gpa }}.</p>
       </body>
   </html>


Assuming we have a student object called joe we can render the template above with the line:  ``t.render(s=joe)``

