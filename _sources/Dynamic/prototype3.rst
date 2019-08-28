Prototype 3 Storing the List in the Browser
===========================================

With this new information about localStorage and how to serialize javascript objects we are now ready to update our application.  The wonderful thing about this next step is that we are adding some major new functionality to our app, but its not going to require a reorganization of our existing code. Lets look at list of steps:

1. Write a new class called LocalStorageSaver with the following capabilities.

   a. Write a saveAll method to serialize our shopping list and save the serialized list to localStorage.
   b. Make this class a client of the model.  So that whenever the model changes we save it.

.. mchoice:: localstore_client

   What is the best way to arrange for our new LocalStorageSaver class to be a client of the model?

   - Make LocalStorageSaver a subclass of ShoppingList

     - No, although this could work it would tightly couple the model to a particular method of persistent storage.

   - Make the LocalStorage object a property of our model.

     - No, although we could make this work as well, its not the best solution for our architecture.

   - Have the LocalStorageSaver object subscribe to the model

     + Corrrect!

The benefit of keeping the LocalStorageSaver class independent is that it now makes it easy for us to save our model without modifying any of the existing model code, and we could even add additional "xxxSaver" classes if we want to store our data some other way. -- We'll eventually have to get there anyway!

.. code-block:: javascript

"use strict"
class LocalStorageSaver {

    constructor(model,lsname) {
        this.lsname = lsname;
        let self = this
        model.subscribe(function(slist, msg) {
            self.saveAll(slist)
        })
        // now restore from localstorage
        let restore_list = JSON.parse(localStorage.getItem(self.lsname))
        for(let vals of restore_list) {
            let it = new Item(vals.name, vals.quantity, vals.priority, vals.store, vals.section, vals.price)
            model.addItem(it)
        }
    }

    saveAll(slist) {
        let ls_list = JSON.stringify(slist.newItems)
        localStorage.setItem(this.lsname, ls_list)
    }
}


**Exercise**  Add this class definition to your project, and make sure you instantiate an instance somewhere.  confirm that the app now remembers your list even after a page refresh.


