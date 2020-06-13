Semantic HTML Tags
==================

Some tags in HTML are designed for you to use in creating a logical structure for your page.  As you have probably noticed many sites have a navigation bar in the header, and have some information about the page in a footer.  Many web pages have sidebars, and of course blogs and many news sites are divided into articles.  Scholarly web sites are divided into parts and sections.

You have probably also noticed that it is pretty easy to tell the different parts of a web page apart because they have a distinct look to them.  In order to give different sections different looks we need to provide some structure within our markup.   This is done by using structural tags as follows:


* article
* aside
* details
* figcaption
* figure
* footer
* header
* main
* mark
* nav
* section
* summary
* time

These tags are all block level tags, but other than that they have no impact on how the page looks without the use of CSS!  Figure 1 illustrates how many of these tags are used to create structure in a page.

.. figure:: Figures/img_sem_elements.gif

   Figure used in accordance with the educational fair use policy of w3schools.com

Let's look at an example that uses some of these tags:

.. activecode:: sem_tags
   :language: html
   
   <html>
   <body>
   <header>
   <p>This is text in the header</p>
   </header>
   <aside>
   <p>This is a side comment</p>
   </aside>
   <article>
   <p>This is some text for an article</p>
   </article>
   <p>Notice that there is nothing special about the location of any of this text.  Without CSS the semantic tags simply divide the document logically</p>
   </body>
   </html>


.. admonition:: Historical Note

   All of the tags mentioned above were added to the HTML5 standard.  Before HTML5 there were only two of these invisible structural tags.  You will see many examples of the use of these tags:
   
   * div
   * span
   
   These tags served the same purpose, usually by using an id or class attribute to indicate their semantic purpose.
   
   
