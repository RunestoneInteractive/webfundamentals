HTML Elements for Interaction
=============================

Building interactive web pages requires a variety of elements that allow your application to interact with the user.  The HTML5 standard provides us with many different elements from which we can construct an application.


Button
------

.. code-block:: html

   <button>Click Me</button>

.. raw:: html

   <div style="display: block;">
   <button>Click Me</button>
   </div>


The Input Tag
-------------

Many of the elements used in constructing a user interface use the ``input`` tag.  All of the ``input`` elements have a common set of attributes, the most important is the ``type`` attribute as that is what determines how the input element will look.

* type
* name
* id
* value


Text Input
----------

.. code-block:: html

   <input type="text" value="changeme" size="40">

.. raw:: html

   <div style="display: block;">
   <input type="text" size="20" value="change me">
   </div>


Password
--------

.. code-block:: html

   <input type="password" value="secret" size="40">

.. raw:: html

   <div style="display: block;">
   <input type="password" size="40" value="change me">
   </div>



Checkbox
--------

.. code-block:: html

   <input type="checkbox" name="group1" value="audi">Audi<br />
   <input type="checkbox" name="group1" value="bmw">BMW<br />
   <input type="checkbox" name="group1" value="mercedes">Mercedes<br />

.. raw:: html

   <div style="display: block">
   <input type="checkbox" name="group1" value="audi">Audi<br />
   <input type="checkbox" name="group1" value="bmw">BMW<br />
   <input type="checkbox" name="group1" value="mercedes">Mercedes<br />
   </div>


Radio
-----

.. code-block:: html

   <input type="radio" name="group1" value="audi">Audi<br />
   <input type="radio" name="group1" value="bmw">BMW<br />
   <input type="radio" name="group1" value="mercedes">Mercedes<br />

.. raw:: html

   <div style="display: block">
   <input type="radio" name="group1" value="audi">Audi<br />
   <input type="radio" name="group1" value="bmw">BMW<br />
   <input type="radio" name="group1" value="mercedes">Mercedes<br />
   </div>

Color
-----

Depending on the browser you are using this will either look like a generic text box or it will appear as a colored block which when you click on it will bring up a color picker.

.. code-block:: html

   <input type="color">

.. raw:: html

   <div style="display: block">
   <input type="color">
   </div>

Range
-----

.. code-block:: html

   <input type="range" min=0 max=255 value=125>

.. raw:: html

   <div style="display: block;">
   <input type="range" min=0 max=255 value=125>
   </div>

Date Stuff
----------

* month
* datetime-local
* week
* time


Drop Down Menus
---------------

.. code-block:: html

   <select id="priority">
       <option>High</option>
       <option>Medium</option>
       <option>low</option>
   </select>
   
.. raw:: html

    <div style="display: block;">
        <select id="priority">
            <option>High</option>
            <option>Medium</option>
            <option>low</option>
        </select>
    </div>