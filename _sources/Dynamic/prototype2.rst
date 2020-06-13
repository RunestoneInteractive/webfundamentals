Our Second Prototype
====================

In this section I'll include the code for the three javascript files that make up our model, view and controller, and we will implement the publish subscribe pattern described in the previous section.

In this code the shopping view subscribes to the model so that when the model changes the view is "automatically updated"  Specifically the View provides the redrawList method to the view as the method to call when new items are added to or removed from the shopping list.

Model Code
----------

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

        get purchased() {
            return this._purchased;
        }

        set purchased(nv) {
            this._purchased = nv;
            alert(`${this.name} was purchased`)
        }



    }

    class Subject {

        constructor() {
            this.handlers = []
        }

        subscribe(fn) {
                this.handlers.push(fn);
            }

        unsubscribe(fn) {
            this.handlers = this.handlers.filter(
                function(item) {
                    if (item !== fn) {
                        return item;
                    }
                }
            );
        }

        publish(msg, someobj) {
            var scope = someobj || window;
            for (let fn of this.handlers) {
                fn(scope, msg)
            }
        }
    }


    class ShoppingList extends Subject {
        constructor() {
            super()
            this.newItems = []
            this.oldItems = [];
        }

        addItem(it) {
            this.newItems.push(it)
            this.publish('newitem', this)
        }
    }


View Code
---------

.. code-block:: javascript

    class ShoppingView {
        constructor(model) {
            // The bind() method creates a new function that, when called, has its this keyword set to the provided value.
            model.subscribe(this.redrawList.bind(this))
        }

        redrawList(shoppingList, msg) {
            let tbl = document.getElementById("shoppinglist")
            tbl.innerHTML = ""
            for (let item of shoppingList.newItems) {
                this.addRow(item, tbl)
            }
        }

        addRow(item, parent) {
            let row = document.createElement("tr")
            row.classList.add(item.priority)
            let cb = document.createElement("input")
            cb.type = "checkbox"
            cb.classList.add("form-control")
            cb.onclick = function() { item.purchased = true; }
            row.appendChild(cb)

            for (let val of ['name', 'quantity', 'store', 'section', 'price']) {
                let td = document.createElement("td")
                td.innerHTML = item[val]
                row.appendChild(td)
            }
            parent.appendChild(row)
        }
    }


Controller Code
---------------

.. code-block:: javascript

    var stores = ['Fareway', 'Ace Hardware', 'Caseys', 'The Hatchery', 'Amundsens']
    var sections = ['Produce', 'Meats', 'Cereal', 'Canned Goods', 'Frozen Foods', 'Dairy', 'Liquor', 'Tools', 'Clothing']

    var shoppingModel = new ShoppingList()
    var myView = new ShoppingView(shoppingModel)

    function clickedon() {
        let rowcolids = ['itemname', 'qty', 'store', 'category', 'price', 'priority']
        let vals = {}
        for (let cid of rowcolids) {
            vals[cid] = document.getElementById(cid).value;
        }
        let it = new Item(vals.itemname, vals.qty, vals.priority, vals.store, vals.category, vals.price)
        shoppingModel.addItem(it)
    }


    function populateSelect(selectId, sList) {
        let sel = document.getElementById(selectId, sList)
        for (let s of sList) {
            let opt = document.createElement("option")
            opt.value = s
            opt.innerHTML = s
            sel.appendChild(opt)
        }
    }

    $(document).ready(function () {
        populateSelect('store', stores)
        populateSelect('category', sections)
    })


Let's trace through precisely what happens when an item is added to the shopping list.

1. User fills out the form with information about the item to be added.
2. User clicks on the Add Item button.  Clicking causes the ``clickedon`` function in the controller to be invoked.

   a. The ``clickedon`` function creates a new ``Item``
   b. Then ``clickedon`` calls ``shoppingModel.addItem`` which adds the newly created item to the model

      i. The ``addItem`` method of the model appends the new item to the list of items.
      ii. Then ``addItem`` calls the ``publish`` method which invokes all of the functions that have registered to know about changes to the model.

         - In this case the only function that is registered for changes is the ``redrawList`` method of the view, which erases and rebuilds the list

This is really kind of beautiful.  The **controller** calls a method which adds a new item to the **model**.  The model then automatically invokes methods that the **view** has told it about in order to update what the user sees.  The beauty is that it is all loosely coupled through the publish / subscribe pattern.  This makes it nice and extendable in case other parts of the view need to be updated in response to other changes in the model.
