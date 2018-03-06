Model View Controller
=====================

Lets critique our first prototype a bit.

* How are we doing with respect to keeping the visual look of the site separate from the programming logic?  Not bad at this point.  The only javascript is simply included through a script tag and the creation of the select boxes as well as the table rows is only connected through the ids of the blank elements.

* When we want to add more functionality such as totaling our costs or sorting our shopping list, do we have a good way of accessing the data?  The answer to this one is an emphatic NO our data is now fully entwined with our html. The only way we have to retrieve our shopping list to do something with it is to iterate over the table rows and extract the values from the tags in each table row.  Ugh!!

Lets fix this second problem right now. The way we are going to do this is to redesign our application to follow the Model View Controller paradigm.  The MVC paradigm is a tried and tested way of making applications that gives you a nice separation of concerns and will solve the problem we identified in our critique.  The following diagram gives you a good idea of what is going on.

.. image:: MVC-Process.svg

We will divide our coding into three distinct blocks:

* Model:  the model will be two classes to represent the primary data structures we want to work with in our application.  An Item class that will represent things we want to put on our shopping list, and a ShoppingList class that will represent the entire list, and be the main point of intersection for our controller.

* View: The view will provide us with an HTML representation of the model.  That is what we have now, but rather than being the **only** place that stores the information the View will now simply be there to provide us with a visual representation of the things that are in our model.  

* Controller: As the diagram shows the user interacts with the controller.  Right now our only 'controller' is the clicked on function.  When a button is clicked  the clickedon function is called to update the table.

In the next revision of our program the controller will no longer directly manipulate the html that we see on the page but rather will manipulate our model.  When a user clicks on the Add button the controller will create an Item and then call a method on our ShoppingList object to add the item to a list.

Here is the code for our new model:

.. code-block:: javascript

    'use strict';
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

    }

    class ShoppingList {
        constructor() {
            this.newItems = []
            this.oldItems = [];
        }

        addItem(it) {
            this.newItems.push(it)
        }
    }


Now, our controller should simply look like this:

.. code-block:: javascript

    var shoppingModel = new ShoppingList()

    function clickedon() {
        let rowcolids = ['itemname', 'qty', 'store', 'category', 'price', 'priority']
        let vals = {}
        for (let cid of rowcolids) {
            vals[cid] = document.getElementById(cid).value;
        }
        let it = new Item(vals.itemname, vals.qty, vals.priority, vals.store, vals.category, vals.price)
        shoppingModel.addItem(it)
    }

Now all the controller does is create a new item and add it to the list.  Nice!

The remaining question is how does the Model let the View know that it has a new item and that new item should be added to the html table so our user can see it there?  We will tackle that problem in the next couple of sections.

