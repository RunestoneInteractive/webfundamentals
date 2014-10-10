Iteration
=========


Iteration allows us to do things many times, or to process a **collection** of elements.  We'll look at collections shortly, for now let us just focus on the
basics of iteration.


Now this is not very exciting, but suppose we want to build a table that has a row for each number from 0 through 9.  


.. activecode:: js_iter1
   :language: javascript
   
   for(i = 0; i < 10; i++) {
       writeln("the number is " + i)
   }
   

Now that was pretty simple, but it illustrates a very important aspect of programming.  The key aspects of the example are:

1.  The for statement,  is the statement that allows us to do things many times.
2.  The number of times we do something is controlled by the three statements:
    1. ``i = 0`` this is our starting value
    2. ``i < 10`` this is our stopping condition.  We will keep doing whatever is inside the for statement until ``i < 10`` is no longer true.
    3.  ``i++`` this is really important as it changes the value of i and allows us to make progress towards the end.  Without this third component, i would never increase and we would do whatever is inside the loop forever.  This is called an **infinite loop**.
    
Now let us look at how we can use the loop to add 10 rows to a table.


.. activecode:: js_iter2
   :language: html

   <html> 
   <table id="mytable"></table>   
   <script>  
   tbl = document.querySelector("#mytable")
   for(i = 0; i < 10; i++) {
       row = document.createElement("tr")
       cell = document.createElement("td")
       cell.innerText = i
       row.appendChild(cell)
       tbl.appendChild(row)
   }

   </script>
   </html>