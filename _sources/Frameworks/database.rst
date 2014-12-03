Persistent Data and Datbases
============================

In the three legged stool of web applications, we have covered both the view and the controller.  We have even built simple apps with very simple models.  But now it is time to look at a real model, and how a database management system is used in a web application.   We will divide this chapter into three modules:

1.  Data Modeling and Creating a Database
2.  Querying the database using Python's DBAPI
3.  Using an Object Relational Mapping layer such as SQLAlchemy

Data Modeling
-------------

Let me begin with the statement that data modeling could be the most important skill you learn in your computer science career.  If you understand your (or your customer's) data, and can effectively communicate to your customer about their data you have already won half the battle.  Data modeling is an excellent communications tool, both to help you uncover hidden requirements and assumptions, and to facilitate good understanding between you and those you are working with.

A data model will help us uncover and describe the entities that are important to our application.  These entities will become the tables in our database.  The things we need to remember about the entities or the attributes of our entities will become the columns in our table.

Lets use an example of a grocery shopping list to illustrate what we mean.  To start out very simply we start to think of the nouns or things that are important to a grocery shopping list.  The following is a list of things related to grocery shopping that you might brainstorm:

* grocery
* price
* item
* 