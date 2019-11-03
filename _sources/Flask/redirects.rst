Redirects and Errors
--------------------

To redirect a user to another endpoint, use the :func:`~flask.redirect`
function; to abort a request early with an error code, use the
:func:`~flask.abort` function::

    from flask import abort, redirect, url_for

    @app.route('/')
    def index():
        return redirect(url_for('login'))

    @app.route('/login')
    def login():
        abort(401)
        this_is_never_executed()

This is a rather pointless example because a user will be redirected from
the index to a page they cannot access (401 means access denied) but it
shows how that works.

By default a black and white error page is shown for each error code.  If
you want to customize the error page, you can use the
:meth:`~flask.Flask.errorhandler` decorator::

    from flask import render_template

    @app.errorhandler(404)
    def page_not_found(error):
        return render_template('page_not_found.html'), 404

Note the ``404`` after the :func:`~flask.render_template` call.  This
tells Flask that the status code of that page should be 404 which means
not found.  By default 200 is assumed which translates to: all went well.

See :ref:`error-handlers` for more details.
