Grid Layout
===========

Earlier we looked at an example of laying out a modern page. CSS now provides us with even more powerful tools for doing page layout than ever before.

the CSS grid layout is a two-dimensional grid-based layout system designed specifically to solve the layout problems that CSS coders have been struggling with for years.


Using grid layout begins with a container element that uses a ``display: grid`` property.  You can then describe what your grid looks like with two additional properties:

* ``grid-template-columns`` how many columns in your grid, and how should these columns be apportioned their space.
* ``grid-template-rows`` how many rows should your grid have and how should their space be appropriated.  (Note its ok to go over the number of rows, and layout will continue to add containers into columns, but the height will be determined automatically.

The layout of grid operates mostly left to right top to bottom, taking the child elements of the container and putting them into their columns first.  When you've used up the first row of columns layout continues on the second row, and so forth.

Lets take a look at a simple example:

.. activecode:: grid_layout_1
    :language: html
    :include: grid_layout_css

    <body>
        <div class="wrapper">
            <div id="d1">
                1
            </div>
            <div id="d2">
                2
            </div>
            <div id="d3">
                3
            </div>
            <div id="d4">
                4
            </div>
            <div id="d5">
                5
            </div>
            <div id="d6">
                6
            </div>
        </div>
    </body>

The style for the example above is here:

.. activecode:: grid_layout_css
    :language: html
    :include: grid_layout_1

    <style>
        .wrapper {
            display: grid;
            grid-template-columns: 33% 33% 34%;
        }

        #d1 {
            font-size: 20pt;
            text-align: center;
            background-color: aqua;
        }
        #d2 {
            font-size: 20pt;
            text-align: center;
            background-color: greenyellow;
        }
        #d3 {
            font-size: 20pt;
            text-align: center;
            background-color: pink;
        }
        #d4 {
            font-size: 20pt;
            text-align: center;
            background-color: orange;
        }
        #d5 {
            font-size: 20pt;
            text-align: center;
            background-color: mintcream;
        }
        #d6 {
            font-size: 20pt;
            text-align: center;
            background-color: maroon;
        }
    </style>

The grid layout has the concept of tracks and grid lines.  In the example above we have defined 3 tracks, one for each column and four grid lines. two on the outside and the two lines separating track 1 from track 2 and another separating track 2 from track 3.  The same concept applies to the rows.

We can use these values to take more control over how and where we want our grid containers to go.  Lets say we want ``#d1`` to span all three columns.  We can add ``grid-column-start: 1;`` and ``grid-column-end: 4;`` as descripters for our ``#d1`` element



.. activecode:: grid_layout_css2
    :language: html
    :include: grid_layout_1

    <style>
        .wrapper {
            display: grid;
            grid-template-columns: 33% 33% 34%;
        }

        #d1 {
            font-size: 20pt;
            text-align: center;
            background-color: aqua;
            grid-column-start: 1;
            grid-column-end: 4;
        }
        #d2 {
            font-size: 20pt;
            text-align: center;
            background-color: greenyellow;
        }
        #d3 {
            font-size: 20pt;
            text-align: center;
            background-color: pink;
        }
        #d4 {
            font-size: 20pt;
            text-align: center;
            background-color: orange;
        }
        #d5 {
            font-size: 20pt;
            text-align: center;
            background-color: mintcream;
        }
        #d6 {
            font-size: 20pt;
            text-align: center;
            background-color: maroon;
        }
    </style>

Notice how it continues to flow the rest of the elements just as you would expect.  The ``grid-row-start`` and ``grid-row-end`` descriptors work the same way.

* Try changing the layout above so that ``#d2`` starts at row 2 and spans al the way to row 4.