Logging
-------

.. versionadded:: 0.3

Sometimes you might be in a situation where you deal with data that
should be correct, but actually is not.  For example you may have
some client-side code that sends an HTTP request to the server
but it's obviously malformed.  This might be caused by a user tampering
with the data, or the client code failing.  Most of the time it's okay
to reply with ``400 Bad Request`` in that situation, but sometimes
that won't do and the code has to continue working.

You may still want to log that something fishy happened.  This is where
loggers come in handy.  As of Flask 0.3 a logger is preconfigured for you
to use.

Here are some example log calls::

    app.logger.debug('A value for debugging')
    app.logger.warning('A warning occurred (%d apples)', 42)
    app.logger.error('An error occurred')

The attached :attr:`~flask.Flask.logger` is a standard logging
:class:`~logging.Logger`, so head over to the official :mod:`logging`
docs for more information.
