Toward Modern Web Development
=============================

A web framework is a software framework designed to simplify web development. Frameworks exist to save you from having to re-invent the wheel and reduce your workload when you are building a new site.

In this chapter we will look at some of the components of a web framework, and introduce some Python packages that implement those components.  Finally, we will introduce the Flask micro-framework which will tie together the individual components into a comprehensive whole.

Some of the components we will consider in the coming chapters include:

* Template Engines
* Object Relational Mapping libraries
* Routing or URL mapping
* Form creation and processing
* controllers that do not force you to write a separate Python program for every request.
* Helper objects for decoding QUERY_STRINGS and managing Cookies and Sessions.

Templates
---------

If you have tried even one server side web project, you may already have recognized that there is a certain amount of tedium in developing pages.  First and formost among these are print statements!  Really, I can hear you say, "we really have to use print statements for everything when we make a web page?"  Although triple quoted strings are certainly one way to reduce some of the tedium, things can get really complicated when you need to concatenate together really big strings that have embedded quotes want to insert values from variables.

To solve this problem all web frameworks include a **template** engine.  Temmplates allow you to create files that are a simple mix of HTML and placeholders.  The template engine fills in the placeholders with values from your application.


Databases
---------

Another big problem that all web frameworks solve is the persistence problem.  Its fine to write applications that have variables, but variables only exist for the life of the program.  Web servers are reliable, but they go down and need to be restarted fairly frequently.  So, there needs to be a way to store and retrieve information from long term storage.  I'm talking about databases here.  The authors of web frameworks realized very early on that web programmers did not want to become database experts in addition to everything else they have they have to know, so web frameworks provide an Object Relational Mapper, that makes it easy to go back and forth between the database and your Python application.

There are also an increasing number of non-relational databases that go under the heading of NOSQL databases that are used in web applications.


Forms Processing
----------------

Creating forms is tedious in the extreme, and it turns out to be quite easy to automate.  Most frameworks therefore provide an easy way to map database tables or simple Python objects to forms.  When one of these automatically generated forms is submitted, the framework can take care of validating the submitted data as well as storing it in the database.

It sounds like there's almost no work left to do!  And that is the point, of frameworks to make it easy to get something minimal up and running very quickly!

Flask
-----

To conclude this introductory section we will look at the Flask framework.  We will take one more lap through the hello world app from the CGI chapter and see how we would write this with a mimum amount of help from the framework.  At the end of all this we'll see how little work it would take to do our full hello world application using all of the components of the framework.

But First...

.. admonition:: Installing a Virtual Environment and Flask

   For your own development purposes it is good to get in the habit of using a virtual environment.  Using Python 3.4 it is really easy.

   1.  Make a Folder in your home directory called Environments
   2.  run the command ``python3 -m venv ~/Environments/flaskenv``
   3.  Now run the command ``. ~/Environments/flaskenv/bin/activate``  This activates the python virtual environment and sets up everything so that you will run a special Python contained in the virtual environment.  Best of all you now have permission to install any third party python packages into your own virtual environment without needing root permission.
   4.  run ``pip install flask``

   After installing flask you can verify that everything is good by running ``pip list`` you should see the following::

       Flask (0.10.1)
       itsdangerous (0.24)
       Jinja2 (2.7.3)
       MarkupSafe (0.23)
       pip (1.5.6)
       setuptools (2.1)
       Werkzeug (0.9.6)



