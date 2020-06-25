Fundamentals of Web Programming
===============================

I have a taught course on web programming for about seven years now.
Not once have I been able to find a textbook that really covered the breadth of materials
that I think should be covered.  So, I started writing this book.  The course has evolved
over the years along the following lines:

1. Basic HTML and CSS -- most college students have not built a web page from scratch
2. Introduction to Javascript -- I've taught this to upper level students so learning Javascript isn't too hard
and this section has always culminated with a midterm-mashup assignment that gets them using an
API from two or more websites.
3. After the midterm we cover how a web server works and old fashioned CGI programming.  The
realization that a simple Python script can create a web page on the fly is a pretty empowering
realization to anyone.
4. I always try to get people to dip their toe into the database waters with simple queries.  Maybe as complicated
as a three table join.
5.  Introduce some kind of web development framework based on WSGI.  I have tried several over the years, but my
recent favorite is Flask because it's simple and doesn't do magical things.

Thats a lot to cram into a single semester and we often end up rushing through some kind of Flask based project
at the end.

Last year we decided to take the first half of the course, HTML, CSS, and Javscript and break it out
into a seven week course for majors and non-majors alike.  This corresponds to Part I of this book.

**Part II, is still very rough,** and I hope to work on extending it and cleaning it up as I prepare to teach
the new web programming course this coming Spring (2016).

I welcome suggestions for content and examples as well as corrections.

Getting Started
===============

We have tried to make it as easy as possible for you to build and use this book.

1. You can see and read this book online at `interactivepython.org <http://interactivepython.org/runestone/static/thinkcspy/index.html>`_

2.  You can build it and host it yourself in just a few simple steps:

    1.  ``pip install -r requirements.txt``  -- Should install everything you need
    2.  ``runestone build`` -- will build the html and put it in ``./build/webfundamentals``
    3.  ``runestone serve``   -- will start a webserver and serve the pages locally from ``./build/webfundamentals``


