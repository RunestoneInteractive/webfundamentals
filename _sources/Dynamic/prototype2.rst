Our Second Prototype
====================

In this section I'll include the code for the three javascript files that make up our model, view and controller.

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
