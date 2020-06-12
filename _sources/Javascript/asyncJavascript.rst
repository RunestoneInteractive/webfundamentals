Asynchronous Programming
========================

Perhaps one of the hardest aspects of prgramming in JavaScript is learning to cope with the asynchronous nature of JavaScript itself.  Javascript can only do one thing at a time.  It is a "single threaded" language.  But what happens when you want to do something that may take some time, usually this involves makeing a call to another server to get data from a database.  Now, you don't just want your program to sit around and wait while the other server does some work, You'd like it to respond to button clicks or whatever else is next on the event queue.  Then when the data comes back you would like your program to deal with the data and update your web page accordingly.

To handle this we return to callback functions.  Just as we first described a callback in :ref:`Events <jsevents>` we return to callback functions here.  When the other server is done with its work, then we need to function to call to continue.  In 2015 the ECMASCRIPT5 standard was released and it introduced a new object for JavaScript called a Promise.  Promises and callbacks solve a similar problem, the difference is that with callbacks, you tell the function what to do when the task completes whereas with promises the function returns a promise to you and you tell the promise what to do when the task completes.

Promises
--------

JavaScript Promises are very much like promises in real life.  If I tell you that I promise I will stop at the grocery store and buy milk on my way home, then you can stop worrying about getting milk and leave it to me.  When I get home with the milk then my promise is fulfilled (resolved in JavaScript terms).  If I mess up and forget to buy the milk or the store is out of milk for some reason then my promise is broken (rejected in JavaScript terms).  With JavaScript you can also specify what you want to have happen when a promise is resolved.  For example, when I arrive home with the milk the next thing to do is get out some cookies and eat them with a nice glass of milk.

We will illustrate this idea of promises using the JavaScript ``fetch`` method. The fetch method is used to get information from a server. When you call ``fetch`` it returns a Promise.  This promise is resolved as soon as the headers are received from the server.  You can then tell the promise what you want done when the request is resolved.  Maybe you want to get the data that is returned and make a graph, or display  it in a table, or show it on a map. If the promise is broken then you may try again, or display a message to the user, or try a whole different backup server.

The Runestone server has an imaginary service that can predict the price of any stock.  You give it a stock symbol and its current price and and it will predict the closing price for the next day it is traded.  The accuracy of this predictor is very suspect, but it gives us something to play with.  Oh, it also only knows how to make predictions for AAPL, GOOG, FB, AMZN and MSFT.  Now making predictions takes a lot of specialized AI software so it may take a while to calculate.  This is why we need an asynchronous interface to deal with it.

If you try the following URL:  https://runestone.academy/runestone/stocks/predict/AAPL it will return something that looks like this: ``{"stock": "AAPL",  "price": 235.87, "date": "2019-10-14"}``  If you look it up you will see that it nailed this prediction perfectly.  But again, the past performance is not necessarily indicative of future performance, your mileage may vary, please don't take this as investment advice.

Using the ``fetch`` method we can have runestone give us back a stock prediction that we can use in our program. We will ask the server to return a prediction for the stock price of Apple and then simply display the prediction to the user.  If the request fails for any reason then we will display an error message to the user.

.. activecode:: ac_async_1
    :language: javascript

    function receiveResponse(resp) {
        writeln('received response')
        return resp.json();
    }

    function receiveJson (prediction) {
        writeln(prediction.stock);
        writeln(prediction.price);
    }

    writeln("sending the request");
    let opts = {
        method: 'GET',
    }

    let myPromise =
        fetch("/runestone/stocks/predict/AAPL", opts)
    let jp = myPromise.then(receiveResponse)
    jp.then(receiveJson)
    jp.catch( (err) => writeln('Error getting prediction, details: ' + err) );
    writeln("the request has been sent");

Now that seems like a lot of code to accomplish a simple task, but I've made it as verbose as possible to make it easier to break down.  Shortly, we will see how to shorten it up considerably.

1.  The call to ``fetch`` sends the request to runestone and immediately returns a promise (``myPromise``).   That promise will resolve when the response headers are returned.  This is partly for security reasons, that we will mention later.
    a.  We have instructed ``myPromise`` to call ``receiveResponse`` using ``myPromise.then(receiveResponse)``.  The ``then`` method is what you use to tell a promise what to do when a promise is resolved successfully.
    b. Below you will see that we can also use ``catch`` to tell our promise how it should respond in the case of an error.
2. The ``receiveResponse`` function returns the value of ``resp.json()`` which itself is a promise (``jp``)!  This is because ``myPromise`` resolves before all the data has arrived, so lots of things could still go wrong.
3.  When the ``jp`` promise resolves then you know that all of the JSON data has arrived successfully.  The ``jp.catch`` method provides us a safety net for the case when any kind of error has occurred in **any step of this process**.  ``receiveJson`` makes no more promises, it simply works with the data.  In this case it just prints out a couple of values, but of course it could do anything you want.

.. parsonsprob:: promiseorder

    Without running the example above, and assuming that the prediction for AAPL is 242.42 put the output in the order you would see it from the previous code.

    -----
    sending the request
    the request has been sent
    received response
    AAPL
    242.42

There are several ways we can reduce the amount of code from the above example, that also illustrate more common JavaScript coding practices.  Let's take a look at a first group of refinements.

.. activecode:: ac_async_2
    :language: javascript

    writeln("sending the request");
    let opts = {
        method: 'GET',
    }

    let myPromise =
        fetch("/runestone/stocks/predict/AAPL", opts)
    let jp = myPromise.then(function (resp) {
        writeln('received response')
        return resp.json();
    })
    jp.then(function (prediction) {
        writeln(prediction.stock);
        writeln(prediction.price);
    })
    jp.catch( (err) => writeln('Error getting prediction, details: ' + err) );
    writeln("the request has been sent");

The first thing we can do is use an anonymous function instead of writing and declaring a function that is only used in one place.  Why clog up the namespace with things that do not need to be there?


The next thing to do is to make use of **promise chaining**  Instead of assigning a promise to a variable, we can attach the ``then`` method to the the original function that generates the promise (``fetch`` in this case) and when the result of a function called inside ``then`` is a promise we can just attach another then like this ``fetch(...).then(...).then(...)``.


.. activecode:: ac_async_3
    :language: javascript

    writeln("sending the request");
    let opts = {
        method: 'GET',
    }

    fetch("/runestone/stocks/predict/AAPL", opts)
    .then(function (resp) {
        writeln('received response')
        return resp.json();
    })
    .then(function (prediction) {
        writeln(prediction.stock);
        writeln(prediction.price);
    })
    .catch( (err) => writeln('Error getting prediction, details: ' + err) );
    writeln("the request has been sent");


This is quite compact, and the promise chaining seems very clean when you get used to it.


Async / Await
-------------

Promises and using ``then`` and ``catch`` can still be very confusing as we are all used to writing code that runs from top to bottom in order, and even experienced coders can get confused sometimes when writing asynchronous code.  In 2016 the ES 7 standard introduced the keywords async and await which makes writing asynchronous code feel a lot more like the synchronous code we are used to writing.

The async keyword is used before a function definition and guarantees that the function will return a Promise.  It also allows you to use the ``await`` keyword inside the function.  To say that sentence in another way:  You cannot use the ``await`` keyword outside of an ``async`` function.  Not from the top level of a script tag, or from the top level of a .js file.

The await keyword pauses the exectuion of the async function until the promise is resolved.  When this hapens the function resumes from the point it left off and the await expression evaluates to the result value of the promise.  More on this later!

Let's see how this simplifies our example.


.. activecode:: ac_async_4
    :language: javascript

    async function getPrediction() {
        writeln("sending the request");
        let opts = {
            method: 'GET',
        }

        let resp = await fetch("/runestone/stocks/predict/AAPL", opts)
        writeln('got response');
        let prediction = await resp.json();
        writeln(prediction.stock);
        writeln(prediction.price);
        writeln("all done");
    }

    writeln("calling getPrediction")
    let p = getPrediction();
    writeln("back -- " + typeof p)

Wow, now that is nice!  It makes the code in the async function very clean and easy to read, but notice that the getPrediciton function itself returns right away!  That is by design as you know that the function itself is going to handle some asynchronous tasks but you want the main program to be able to go on and handle the next event.

The promises interface has two other methods worth exploring.  ``Promise.all`` and ``Promise.race``.   Promise.all allows you to have a number of different promises active and then wait for all of them to complete.  In fact this all interface is used in the activecode widget in this very book.  When a page loads and you press the load history button several asynchronous tasks are kicked off.  But if you press the Run button before all of them are done, then the history can get out of order.  So, the run button is disabled and when all the tasks are complete it is re-enabled.

Let's look at an example of ``Promise.all`` in action, by kicking off requests for predictions for all of our stocks.

.. activecode:: ac_async_5
    :language: javascript

    async function getPrediction(stock) {
        writeln("sending the request");
        let opts = {
            method: 'GET',
        }
        let resp = await fetch(`/runestone/stocks/predict/${stock}`, opts)
        writeln(`got response for ${stock}`);
        return resp.json();
    }

    let promiseList = [];
    for (let stock of ["AAPL", "GOOG", "FB", "AMZN", "MSFT"]) {
        promiseList.push(getPrediction(stock))
    }

    Promise.all(promiseList).then(function(plist) {
            writeln("all promises complete");
            for (let p of plist) {
                writeln(`${p.stock}, ${p.price}`)
            }
    });

Promises in Depth
-----------------

In this section you will learn how to make your own promises (and hopefully not break them!)  The promise constructor takes a function as an argument.  That function in turn takes two parameters, each of them functions: one function for when the promise is resolved and another for when the promise is rejected.  Most often the function you pass is an anonymous function as it will be called immediately as the new Promise is being made.  Let's look at a fun example.  Write a function to generate the nth fibonacci number.  If the number is odd we will resolve the promise and if the number is even we'll reject it.

.. activecode:: promise_1
    :language: javascript

    async function fibb(n) {
        let p = new Promise(function (resolve, reject) {
            let a = 0;
            let b = 1;
            let c = 0;
            for (let i = 0; i < n; i++) {
                c = a + b;
                a = b;
                b = c;
            }
            if (c % 2 == 0) {
                reject(c);
            } else {
                resolve(c);
            }
        }
        return p;
    }

    fibb(1)
    .then( (r) => writeln(r) )
    .catch( (r) => writeln("rejected ", r) )


