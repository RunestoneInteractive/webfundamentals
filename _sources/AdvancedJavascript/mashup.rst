Interacting with Other Services
===============================

Many websites make their data available for others to use. For example Amazon makes its information about products available, Google allows you to add information to your calendar through your own program, Yelp makes their reviews available, and `many more! <https://github.com/toddmotto/public-apis>`_ are available for free!  These data sources are often referred to as **Web APIs**.  Once a Javascript program has the data it is free to display that data in your browser in many different ways, or even to combine it with other data from other sites in what we call a mashup.

The key to interacting with other services is to have an efficient way to exchange data.  Using the HTTP protocol this data must be plain text.  One way to think about this is in terms of calling a remote function.  The name of the function is the URI.  But how do you pass parameters to this remote function?  There are two ways that a browser can send data to a server.  

* As part of the URL known as a **QUERY_STRING**
* In the **body** of an HTTP request.

Query String Parameters
-----------------------

The query string is used to send data from the browser to the server when an HTTP GET request is made.  As the name suggests it is a special string that is appended to the end of the URL.  You have probably seen many query strings while using the web.  Here is an example:

::

    http://example.com/api/getdata?id=1234&date=now&apikey=1234567


In the example above, the query string is everything after the `?`.  the string is composed of key value pairs separated by the `&` character.  In the example above we have the following key value pairs

* id=1234
* date=now
* apikey=1234567

Notice that the syntax is very regular to make it easy for a program to take the string and split it into the key value pairs.  In the early days of web programming the query string was provided to the web application in the form of an environment variable. The program had to split the string into key value pairs on its own.  In modern web frameworks the query string is automatically processed and provided to the program in the form of a dictionary.

Check your Understanding
~~~~~~~~~~~~~~~~~~~~~~~~

.. activecode:: qs_ex1
    :language: python

    Write a python function that given a URL like `http://example.com/api/getdata?id=1234&date=now&apikey=1234567` returns a dictionary containing the correct keys and values.
    ~~~~
    def query_string_parser(qs):
        # your code Here


.. activecode:: qs_ex2
    :language: javascript

    Write a Javascript function that given a URL like `http://example.com/api/getdata?id=1234&date=now&apikey=1234567` returns a dictionary containing the correct keys and values.
    ~~~~
    function query_string_parser(qs) {
        // your code Here
    }

Javascript Object Notation (JSON)
---------------------------------

What if you want to pass more complicated data to the web api?  What if you have more data to pass to the api than you can do as part of the URL?  In that case you can send the data in the body of the http request.

Since we need to adhere to the HTTP protocol any large data or any complex data objec needs to be turned into a string before it can be sent as part of the body.  The process of turning an object from a program into a string is known as **serialization**.  Web programming uses two main formats to serialize data: XML and JSON.  JSON is highly convenient and is much more widely used today than XML, so we will focus on JSON.

Most of what you need to know about JSON is the two primary methods of the JSON object:  `stringify` and `parse`.  The `stringify` method takes a Javascript object and turns it into a string.  The `parse` method takes a string and turns it into a Javascript object.  There are some important limitations on what can and cannot be stringified.  For example, functions cannot be stringified, dates will be converted into strings, but there is no way to convert them back into Date objects again.

.. activecode:: json_ex1
    :language: javascript

    x = [1, 2, 3.1415, "Hello World"]
    y = {first_name: "Joe", salary: 104000.50 }

    sval = JSON.stringify(y)
    writeln(sval)
    sobj = JSON.parse(sval)
    writeln(sobj)


XMLHTTPRequest

fetch

