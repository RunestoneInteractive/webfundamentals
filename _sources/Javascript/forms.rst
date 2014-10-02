HTML Elements for Interaction
=============================


Common attributes
-----------------

* type
* name
* id
* value


Button
------

.. code-block:: html

   <button>Click Me</button>

.. raw:: html

   <div style="display: block;">
   <button>Click Me</button>
   </div>

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
