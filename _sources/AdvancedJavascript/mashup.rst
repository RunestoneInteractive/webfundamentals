Interacting with Other Services
===============================

One of the most powerful aspects of Javascript is its ability to communicate with other services to retrieve data.  For example weather information, sports scores, stock data and much more.  Once a Javascript program has the data it is free to display that 
data in your browser in many different ways.

The key to interacting with other services is to have an efficient way to exchange data.  Using the HTTP protocol this data must be plain text.  There are two ways that a browser can send data to a server.  

* As part of the URL known as a QUERY_STRING
* In the **body** of an HTTP request.

Query String Parameters
-----------------------

The Query string is used to send data from the browser to the server when an HTTP GET request is made.  As the name suggests it is a special string that is appended to the end of the URL.  You have probably seen many query strings while using the web.  Here is an example:

::

    http://example.com/api/getdata?id=1234&date=now&apikey=1234567


In the example above, the query string is everything after the `?`.  the string is composed of key value pairs separated by the `&` character.  In the example above we have the following key value pairs

* id=1234
* date=now
* apikey=1234567

Notice that the syntax is very regular to make it easy for a program to take the string and split it into the key value pairs.



Javascript Object Notation
--------------------------



XMLHTTPRequest

fetch

