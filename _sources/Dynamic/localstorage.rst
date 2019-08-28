Serializing and LocalStorage
============================

Now we have a really well architected application.  But it is still lacking one big feature.  Persistence. Each time we bring up our web page, or even refresh the page, our list dissappears!  That is bad and nobdy is going to buy our app if they have to start over from the beginning each time.  What we need is a way to store the data.  Our first step on the journey to persistence is to make use of the ``localStorage`` of the browser.  Before we dive into a new prototype we need to learn about two new concepts.

* localStorage
* JavaScript Object Notation (JSON)


Using JavaScript Object Notation (JSON)
---------------------------------------

When you exchange messages between the browser and the server those messages are plain text messages.  However if you have an object in memory, such as a number or a Javascript object or a Python dictionary, those objects are stored in memory in a non-text format (binary).  In order for the browser and the server to share information the in-memory objects must be **serialized**.  Serialization means that an object is converted into a string.

JSON is an important standard for serializing objects.  Most programming languages have a library or module that supports serializing an object to JSON as well as the reverse process -- **deserialization** -- of converting a JSON string back to a native object.  JSON is nice because it is easy for humans to read, and for many programming languages JSON strings are easy to convert into native formats.  If you know a bit of Python you will see that many things look just like dictionaries.  The same is true for JavaScript, but in JavaScript we don't call them dictionaries we just call them objects.

Here is an activecode example.  The primary methods of the JSON object are ``stringify`` and ``parse``.  The stringify method takes an object as a parameter and returns a JSON string.

.. activecode:: json_javascript
    :language: javascript

    x = JSON.stringify([1,2,3.1415, 4])
    write("x is a")
    writeln(typeof x)
    writeln(x)

    y = JSON.parse(x)
    write("y is a ")
    writeln(typeof y)
    writeln(y)
    y.push(5)
    writeln(y)

Notice that there is nothing to import, the JSON object is always available for you to use.

Python is very similar, but the names of the methods are different.  In python you call the ``dumps`` method to serialize an object, and you call ``loads`` to deserialize the string to an object.

.. activecode:: json_python

    import json

    print(json.dumps({'foo': 1, 'bar':2}))
    x = json.dumps([1,2,3,4])
    print("x is a ", type(x))
    print(x)

    y = json.loads(x)
    print("y is a ", type(y))
    y.append(5)
    print(y)

.. warning::

    Not everything can be serialized!  For example, functions and methods cannot be serialized.


For custom objects, that is instances of classes that we create, the default behavior for JSON.stringify is to serialize the properties of the object but not the methods.

For example, take the Item class from our shopping list application.  If we serialize this using ``JSON.stringify`` we will get an object literal that contains the properties name, quantity, priority, store, section, etc.  But none of the methods will be serialzed.

.. activecode:: json_class
    :language: javascript

    class Item {
        constructor(name, quantity, priority, store, section, price) {
            this.name = name;
            this.quantity = quantity;
            this.priority = priority;
            this.store = store;
            this.section = section;
            this.price = price;

            this._purchased = false;
        }

        plainMethod() {
            alert("hello from a plain method");
        }

        get purchased() {
            return this._purchased;
        }

        set purchased(nv) {
            this._purchased = nv;
            alert(`${this.name} was purchased`)
        }

    }

    x = new Item('bread', 1, 'High', 'Fareway', 'Bakery', 3.99);
    writeln(x.constructor.name)

    y = JSON.stringify(x)
    writeln(y)

    z = JSON.parse(y)
    writeln(z)
    writeln(z.constructor.name)
    z.purchased = 10  // Note no alert!
    z.plainMethod() // Error!!

If we want our object to have some special behavior when we serialze it, we can write a method for our object called ``toJSON``  The method takes no parameters and returns a string. Note that this string should be deserializable by the ``JSON.parse`` method.

.. fillintheblank:: json_types

    In the above example the type of x is |blank| and the type of  z is |blank|.

    - :Item: Is the correct answer
      :Object: Well, it is an Object but be more specific.
      :x: Try running the code and looking at the output.

    - :Object: Is the correct answer
      :Item: Is not correct.  JSON has no way to remember the  "user defined type" of an object.
      :x: Try running the code and looking at the output.



Using the localStorage Object
-----------------------------

Before HTML5 the only way to store data in the browser was in a cookie.  That had a lot of limits in terms of size, and cookies are sent to the server with each request, so they were sent out into the internet over a potentially unsecure connection.  In HTML5 localStorage was added to accomodate the needs to keep information persistent, and web storage objects were created.

There are two main web storage objects:

* localStorage can hold at least 5MB of data with no expiration date.
* sessionStorage stores data for one session -- data is erased with the browser tab is closed.


localStorage is subject to some security constraints.  Only pages from the same origin and protocol can access a local storage object.  This prevents javascript on a page loaded from site A and javascript on a page loaded from site B from sharing a localstorage object.  It also means that a page loaded over http from site A and a page loaded over https from site A will also be unable to share.  Practically speaking it also means that if you are testing your page using file:///page/to/page that your local storage will not be shareable when you load it over either http or https.

Using localStorage is as easy as using a python dictionary or a key value lookup on a javascript object.  The difference is that the keys and the values you store in localStorage must be strings.   Good thing you just learned about JSON!

The localStorage object has three important methods:

* ``localStorage.setItem(key, value)``
* ``localStorage.getItem(key)``
* ``localStorage.removeItem(key)``

You can also access a key in localStorage directly using ``localStorage.key``

Run the following example a few times.

.. activecode:: localstore_1
    :language: javascript

    counter = localStorage.counter
    writeln("counter is " + counter);
    if (! counter) {
        counter = 1
    } else {
        counter += 1
    }
    localStorage.counter = counter
    writeln("counter is now " + localStorage.counter)


Do you see anything wrong?  Now reload the page and run it again.  Notice that it keeps counting from where it left off.

**Exercise** Fix the counter so that it counts using the decimal number system.




