Fundamentals of Web Programming
===============================

I have a taught course on web programming for about seven years now.
Not once have I been able to find a textbook that really covered the breadth of materials
that I think should be covered.  So, I started writing this book.  The course has evolved
over the years along the following lines:

1. Basic HTML and CSS -- most college students have not built a web page from scratch
2. Introduction to Javascript -- I've taught this to upper level students so learning Javascript isn't too hard and this section has always culminated with a midterm-mashup assignment that gets them using an API from two or more websites.
3. After the midterm we cover how a web server works and old fashioned CGI programming.  The realization that a simple Python script can create a web page on the fly is a pretty empowering realization to anyone.
4. I always try to get people to dip their toe into the database waters with simple queries.  Maybe as complicated as a three table join.
5. Introduce some kind of web development framework based on WSGI.  I have tried several over the years, but my recent favorite is Flask because it's simple and doesn't do magical things.

That's a lot to cram into a single semester and we often end up rushing through some kind of Flask based project
at the end.

Last year we decided to take the first half of the course, HTML, CSS, and Javascript and break it out
into a seven week course for majors and non-majors alike.  This corresponds to Part I of this book.

**Part II, is still very rough,** and I hope to work on extending it and cleaning it up as I prepare to teach
the new web programming course this coming Spring (2016).

I welcome suggestions for content and examples as well as corrections.

Getting Started
===============

We have tried to make it as easy as possible for you to build and use this book.

1. You can see and read this book online at `runestone.academy <https://runestone.academy/runestone/books/published/thinkcspy/index.html>`_

2. You can build it and host it yourself in just a few simple steps:

.. code:: bash

    # To install everything you need
    $ pip install -r requirements.txt
    # Build the HTML and put it in ./build/webfundamentals
    $ runestone build
    # Start a web server and serve the pages locally from ./build/webfundamentals
    $ runestone serve

