.. Copyright (C) 2011-2012 James Rowe <jnrowe@gmail.com>
                           Michael Basnight <mbasnight@gmail.com>
                           modocache <modocache@gmail.com>

   This file is part of python-github2, is licensed under the 3-clause BSD
   License.  See the LICENSE file in the top distribution directory for the full
   license text.

.. module:: github2.client

Creating a client
=================

.. autoclass:: github2.client.Github
   :exclude-members:
    get_network_meta, get_network_data, get_all_blobs, get_blob_info, get_tree

Examples
--------

There are three ways to authenticate to the GitHub API.  If you want to use your
username and API token, use::

    >>> from github2.client import Github
    >>> github = Github(username="ask", api_token=".......")

If you authenticated to GitHub using their `OAuth service`_, pass in the OAuth
access token::

    >>> github = Github(access_token="........")

.. note::
   You can retrieve the user data for an OAuth authenticated user with
   ``github.users.show("")``.

Or for an unauthenticated connection::

    >>> github = Github()

The package supports caching of GitHub responses by adding a ``cache`` keyword
during setup::

    >>> github = Github(username="ask", api_token=".......", cache="cache_dir")

API calls are limited by github.com to 1 per second by default.  To have the
``Github`` client enforce this and avoid rate limit errors, pass
``requests_per_second`` in::

    >>> from github2.client import Github
    >>> github = Github(username="ask", api_token=".......",
    ...                 requests_per_second=1)

By default, :pypi:`httplib2 (0.7.4)` will use the proxies set in the
:envvar:`http_proxy` andr :envvar:`https_proxy` environment variables.  This
means that well configured systems shouldn't need any manual configuration for
proxy support.

If you wish to manually configure a HTTP proxy you can pass in the
``proxy_host`` and ``proxy_port`` settings to enable it.  The default for
``proxy_port``, if not given, is 8080::

    >>> from github2.client import Github
    >>> github = Github(username="ask", api_token=".......",
    ...                 proxy_host="my.proxy.com", proxy_port=9000)

You may specify a GitHub Enterprise URL by passing in the ``github_url``
setting.  If you do not specify ``github_url``, requests will be made to
https://github.com/.

    >>> from github2.client import Github
    >>> github = Github(username="modocache", api_token=".......",
    ...                 github_url="http://your-github-enterprise-url.com/")

.. _OAuth service: http://develop.github.com/p/oauth.html
