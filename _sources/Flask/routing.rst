Routing
-------

Modern web applications use meaningful URLs to help users. Users are more
likely to like a page and come back if the page uses a meaningful URL they can
remember and use to directly visit a page.

Use the :meth:`~flask.Flask.route` decorator to bind a function to a URL. ::

    @app.route('/')
    def index():
        return 'Index Page'

    @app.route('/hello')
    def hello():
        return 'Hello, World'

You can do more! You can make parts of the URL dynamic and attach multiple
rules to a function.

Variable Rules
``````````````

You can add variable sections to a URL by marking sections with
``<variable_name>``. Your function then receives the ``<variable_name>``
as a keyword argument. Optionally, you can use a converter to specify the type
of the argument like ``<converter:variable_name>``. ::

    @app.route('/user/<username>')
    def show_user_profile(username):
        # show the user profile for that user
        return f'User {username}'

    @app.route('/post/<int:post_id>')
    def show_post(post_id):
        # show the post with the given id, the id is an integer
        return f'Post {post_id}'

    @app.route('/path/<path:subpath>')
    def show_subpath(subpath):
        # show the subpath after /path/
        return f'Subpath {subpath}'

Converter types:

========== ==========================================
``string`` (default) accepts any text without a slash
``int``    accepts positive integers
``float``  accepts positive floating point values
``path``   like ``string`` but also accepts slashes
``uuid``   accepts UUID strings
========== ==========================================

Unique URLs / Redirection Behavior
``````````````````````````````````

The following two rules differ in their use of a trailing slash. ::

    @app.route('/projects/')
    def projects():
        return 'The project page'

    @app.route('/about')
    def about():
        return 'The about page'

The canonical URL for the ``projects`` endpoint has a trailing slash.
It's similar to a folder in a file system. If you access the URL without
a trailing slash, Flask redirects you to the canonical URL with the
trailing slash.

The canonical URL for the ``about`` endpoint does not have a trailing
slash. It's similar to the pathname of a file. Accessing the URL with a
trailing slash produces a 404 "Not Found" error. This helps keep URLs
unique for these resources, which helps search engines avoid indexing
the same page twice.


.. _url-building:

URL Building
````````````

To build a URL to a specific function, use the :func:`~flask.url_for` function.
It accepts the name of the function as its first argument and any number of
keyword arguments, each corresponding to a variable part of the URL rule.
Unknown variable parts are appended to the URL as query parameters.

Why would you want to build URLs using the URL reversing function
:func:`~flask.url_for` instead of hard-coding them into your templates?

1. Reversing is often more descriptive than hard-coding the URLs.
2. You can change your URLs in one go instead of needing to remember to
   manually change hard-coded URLs.
3. URL building handles escaping of special characters and Unicode data
   transparently.
4. The generated paths are always absolute, avoiding unexpected behavior
   of relative paths in browsers.
5. If your application is placed outside the URL root, for example, in
   ``/myapplication`` instead of ``/``, :func:`~flask.url_for` properly
   handles that for you.

For example, here we use the :meth:`~flask.Flask.test_request_context` method
to try out :func:`~flask.url_for`. :meth:`~flask.Flask.test_request_context`
tells Flask to behave as though it's handling a request even while we use a
Python shell. See :ref:`context-locals`.

.. code-block:: python

    from flask import url_for

    @app.route('/')
    def index():
        return 'index'

    @app.route('/login')
    def login():
        return 'login'

    @app.route('/user/<username>')
    def profile(username):
        return f'{username}\'s profile'

    with app.test_request_context():
        print(url_for('index'))
        print(url_for('login'))
        print(url_for('login', next='/'))
        print(url_for('profile', username='John Doe'))

.. code-block:: text

    /
    /login
    /login?next=/
    /user/John%20Doe


HTTP Methods
````````````

Web applications use different HTTP methods when accessing URLs. You should
familiarize yourself with the HTTP methods as you work with Flask. By default,
a route only answers to ``GET`` requests. You can use the ``methods`` argument
of the :meth:`~flask.Flask.route` decorator to handle different HTTP methods.
::

    from flask import request

    @app.route('/login', methods=['GET', 'POST'])
    def login():
        if request.method == 'POST':
            return do_the_login()
        else:
            return show_the_login_form()

If ``GET`` is present, Flask automatically adds support for the ``HEAD`` method
and handles ``HEAD`` requests according to the `HTTP RFC`_. Likewise,
``OPTIONS`` is automatically implemented for you.

.. _HTTP RFC: https://www.ietf.org/rfc/rfc2068.txt

Static Files
------------

Dynamic web applications also need static files.  That's usually where
the CSS and JavaScript files are coming from.  Ideally your web server is
configured to serve them for you, but during development Flask can do that
as well.  Just create a folder called :file:`static` in your package or next to
your module and it will be available at ``/static`` on the application.

To generate URLs for static files, use the special ``'static'`` endpoint name::

    url_for('static', filename='style.css')

The file has to be stored on the filesystem as :file:`static/style.css`.