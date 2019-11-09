Accessing Databases from Python
===============================

Python has a standard `database API <https://docs.python.org/2/library/sqlite3.html>`_ that will work for nearly any relational database, and it is quite easy to use, but not nearly as easy as the `records <https://www.kennethreitz.org/essays/introducing-records-just-write-sql>`_ package by Kenneth Reitz.


**Records is a very simple, but powerful, library for making raw SQL queries
to most relational databases.**

Just write SQL. No bells, no whistles. This common task can be
surprisingly difficult with the standard tools available.
This library strives to make this workflow as simple as possible,
while providing an elegant interface to work with your query results.

*Database support includes RedShift, Postgres, MySQL, SQLite, Oracle, and MS-SQL (drivers not included).*

----------

The Basics
----------
We know how to write SQL, so let's send some to our database:

.. code:: python

    import records

    db = records.Database('postgres://...')
    rows = db.query('select * from active_users')    # or db.query_file('sqls/active-users.sql')


Grab one row at a time:

.. code:: python

    >>> rows[0]
    <Record {"username": "model-t", "active": true, "name": "Henry Ford", "user_email": "model-t@gmail.com", "timezone": "2016-02-06 22:28:23.894202"}>

Or iterate over them:

.. code:: python

    for r in rows:
        print(r.name, r.user_email)

Values can be accessed many ways: ``row.user_email``, ``row['user_email']``, or ``row[3]``.

Fields with non-alphanumeric characters (like spaces) are also fully supported.

Or store a copy of your record collection for later reference:

.. code:: python

    >>> rows.all()
    [<Record {"username": ...}>, <Record {"username": ...}>, <Record {"username": ...}>, ...]

If you're only expecting one result:

.. code:: python

    >>> rows.first()
    <Record {"username": ...}>

Other options include ``rows.as_dict()`` and ``rows.as_dict(ordered=True)``.
