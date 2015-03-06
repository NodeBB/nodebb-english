Configuring apache as a proxy
=============================

*Note: This requires Apache v2.4.x or greater. If your version of Apache is lower, please see :doc:`Apache v2.2.x Instructions <proxies/apache2.2>`*

Enable the necessary modules
-----------------------------

1. sudo a2enmod proxy
2. sudo a2enmod proxy_http
3. sudo a2enmod proxy_wstunnel

Add the config to Apache
-----------------------------

The next step is adding the configuration to your ``virtualhost.conf`` file, typically located in ``/etc/apache2/sites-available/``.
The below configuration assumes you've used 4567 (default) port for NobeBB installation. It also assumes you have the bind address
set to 127.0.0.1.

.. code::

    ProxyRequests off

    <Proxy *>
        Order deny,allow
        Allow from all
    </Proxy>
    ProxyPass /socket.io/1/websocket ws://127.0.0.1:4567/socket.io/1/websocket
    ProxyPassReverse /socket.io/1/websocket ws://127.0.0.1:4567/socket.io/1/websocket

    ProxyPass /socket.io/ http://127.0.0.1:4567/socket.io/
    ProxyPassReverse /socket.io/ http://127.0.0.1:4567/socket.io/

    ProxyPass / http://127.0.0.1:4567/
    ProxyPassReverse / http://127.0.0.1:4567/


The last thing you need to be sure of is that the ``config.json`` in the NodeBB folder defines the node.js port outside of the url:



Example nodebb/config.json
-----------------------------

.. code:: json

    {
        "url": "http://www.yoursite.com",
        "port": "4567",
        "secret": "55sb254c-62e3-4e23-9407-8655147562763",
        "database": "redis",
        "redis": {
            "host": "127.0.0.1",
            "port": "6379",
            "password": "",
            "database": "0"
        }
    }


**Change the domain and dont use the secret in the example above.**
