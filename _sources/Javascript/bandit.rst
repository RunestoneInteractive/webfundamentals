Javascript Project Slot Machine
-------------------------------

.. image:: Figures/cherry.png
   :width: 100px

.. image:: Figures/seven.png
   :width: 100px
   
.. image:: Figures/watermellon.png
   :width: 100px
   
.. image:: Figures/bell.png
   :width: 100px

.. image:: Figures/bar.png
   :width: 100px
   
.. image:: Figures/diamond.png
   :width: 100px

Let's go to Vegas.   In this section we are going to create our own video slot machine.  Like all web projects we will start simple and work our way up to a more complicated project.  Ultimately what we build is going to look like the following:

Let's start by displaying one of two possible slot machine images, that we will randomly select.

.. activecode:: slot_1
   :language: javascript
   
   getImage = function() {
      imgarray = Array("../_images/seven.png", "../_images/watermellon.png",
      "../_images/cherry.png", "../_images/bell.png",
      "../_images/diamond.png", "../_images/bar.png");
      
      rNum = Math.floor(Math.random()*imgarray.length);
      return imgarray[rNum];
   }
   
   d = document.getElementById("slot_1_js");
   iTag = document.createElement("img");
   iTag.src = getImage();
   d.innerHTML = "";
   d.appendChild(iTag);

<div id="slot_1_js">

.. raw:: html

   <div id="slot_1_js"></div>

</div>


.. activecode:: slot_2
   :language: javascript
   
   count = 0;
   
   getImage = function() {
      imgarray = Array("../_images/seven.png", "../_images/watermellon.png",
      "../_images/cherry.png", "../_images/bell.png",
      "../_images/diamond.png", "../_images/bar.png");
      
      rNum = Math.floor(Math.random()*imgarray.length);
      return imgarray[rNum];
   }
   
   swapImage = function() {
       d = document.getElementById("slot_2_js");
       iTag = document.createElement("img");
       iTag.src = getImage();
       d.innerHTML = "";
       d.appendChild(iTag);
       count++;
       if(count > 50) {
           window.clearInterval(intId,100);
       }
    }
    
    intId = window.setInterval(swapImage)

<div id="slot_2_js">

.. raw:: html

   <div id="slot_2_js"></div>

</div>
