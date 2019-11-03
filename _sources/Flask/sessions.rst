.. _sessions:

Sessions
--------

In addition to the request object there is also a second object called
:class:`~flask.session` which allows you to store information specific to a
user from one request to the next.  This is implemented on top of cookies
for you and signs the cookies cryptographically.  What this means is that
the user could look at the contents of your cookie but not modify it,
unless they know the secret key used for signing.

In order to use sessions you have to set a secret key.  Here is how
sessions work::

    from flask import session

    # Set the secret key to some random bytes. Keep this really secret!
    app.secret_key = b'_5#y2L"F4Q8z\n\xec]/'

    @app.route('/')
    def index():
        if 'username' in session:
            return f'Logged in as {session["username"]}'
        return 'You are not logged in'

    @app.route('/login', methods=['GET', 'POST'])
    def login():
        if request.method == 'POST':
            session['username'] = request.form['username']
            return redirect(url_for('index'))
        return '''
            <form method="post">
                <p><input type=text name=username>
                <p><input type=submit value=Login>
            </form>
        '''

    @app.route('/logout')
    def logout():
        # remove the username from the session if it's there
        session.pop('username', None)
        return redirect(url_for('index'))

.. admonition:: How to generate good secret keys

    A secret key should be as random as possible. Your operating system has
    ways to generate pretty random data based on a cryptographic random
    generator. Use the following command to quickly generate a value for
    :attr:`Flask.secret_key` (or :data:`SECRET_KEY`)::

        $ python -c 'import os; print(os.urandom(16))'
        b'_5#y2L"F4Q8z\n\xec]/'

A note on cookie-based sessions: Flask will take the values you put into the
session object and serialize them into a cookie.  If you are finding some
values do not persist across requests, cookies are indeed enabled, and you are
not getting a clear error message, check the size of the cookie in your page
responses compared to the size supported by web browsers.

Besides the default client-side based sessions, if you want to handle
sessions on the server-side instead, there are several
Flask extensions that support this.

Message Flashing
----------------

Good applications and user interfaces are all about feedback.  If the user
does not get enough feedback they will probably end up hating the
application.  Flask provides a really simple way to give feedback to a
user with the flashing system.  The flashing system basically makes it
possible to record a message at the end of a request and access it on the next
(and only the next) request.  This is usually combined with a layout
template to expose the message.

To flash a message use the :func:`~flask.flash` method, to get hold of the
messages you can use :func:`~flask.get_flashed_messages` which is also
available in the templates.  Check out the :ref:`message-flashing-pattern`
for a full example.
