Helper Objects
==============

Array
-----

An Array is used to hold a collection of elements. For example, if we wanted to work with all of the ``li`` elements in a list, we would keep track of them all by keeping them in an Array.  An array allows us to work with each element in turn because each element in the array can be accessed by its number.


Consider the following list.

.. raw:: html

   <ul>
      <li>Luther</li>
      <li>Coe</li>
      <li>Simpson</li>
      <li>Central</li>
      <li>Wartburg</li>
   </ul>


The first thing in our list is Luther: its position in the list is 0.  The second thing on the list is Coe: its position is 1. The last thing on the list (appropriately) is  Wartburg: its position is 4.

We can get the elements from the list and put them in an array using the ``querySelectorAll`` funciton.


.. activecode:: helper_array_1
   :language: html
   
   <html>
   <body>
     <ul>
        <li>Luther</li>
        <li>Coe</li>
        <li>Simpson</li>
        <li>Central</li>
        <li>Wartburg</li>
     </ul>
     <script>
         theList = document.querySelectorAll('li')
         alert(theList[0].innerText)
     </script>
   </body>
   </html>


We can combine iteration and arrays to work with each element in an array as follows:

.. activecode:: helper_array_2
   :language: html
   
   <html>
   <body>
     <ul>
        <li>Luther</li>
        <li>Coe</li>
        <li>Simpson</li>
        <li>Central</li>
        <li>Wartburg</li>
     </ul>
     <script>
         theList = document.querySelectorAll('li')
         for(i=0; i< theList.length; i++) {
           alert(theList[i].innerText)
         }
     </script>
   </body>
   </html>


String
------
