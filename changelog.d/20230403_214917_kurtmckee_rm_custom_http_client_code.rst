Breaking changes
----------------

*   URLs using a ``feed://`` scheme are no longer handled by feedparser.

    Please convert such URLs to ``https://`` (or ``http://``) URLs
    before passing them to feedparser.
    This removes an ancient, undocumented internal fallback to HTTP.

*   URLs using a ``file://`` scheme are no longer handled by feedparser.

    Please convert these to standard filesystem paths
    before passing the path to feedparser.
    This removes a potential vector by which local paths might be unexpectedly accessed.

*   URLs using an ``ftp://`` scheme are no longer handled by feedparser.

    Please use another package to transport data via FTP
    before passing the content to feedparser.
    This removes an untested code path.

*   ``feedparser.parse()`` no longer uses ``urllib2`` under the hood.

    As a consequence, these parameters have changed semantics:

    *   ``modified``: passed in the request as-is and must be of type ``str``.
    *   ``handlers``: has been removed and is no longer accepted.

    Some missing functionality is already supported by the ``requests`` package
    in a different way (e.g. detecting ``HTTP_PROXY`` from the environment). If
    you still need to customize the request beyond that, then please use an HTTP
    client to request a URL and pass the resulting content to
    ``feedparser.parse()``.

*   TLS certificates are now verified
    due to default behavior in the ``requests`` package.

    If you need to disable certificate verification,
    please use an HTTP client like the ``requests`` package to request a URL,
    then pass the resulting content to ``feedparser.parse()``.

Changed
-------

*   Replace feedparser's custom HTTP client code with the ``requests`` package.
*   Set the ``status`` result key to the final HTTP status code returned.

    Previously, the ``status`` key would contain intermediary HTTP status codes.

*   Timeout after 10 seconds when requesting a feed from a URL.

Removed
-------

*   ``feedparser.parse()`` no longer accepts parameters that customize HTTP requests.

    See the "Breaking changes" section for more information.

*   URLs using a ``feed://``, ``file://``, or ``ftp://`` scheme are no longer supported.

    See the "Breaking changes" section for more information.
