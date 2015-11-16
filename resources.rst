Developer's Resources
=====================


.. note::

	This section is under construction.


Core
----

* `Building a new Admin Page <https://github.com/NodeBB/NodeBB/wiki/How-to-build-a-new-Admin-Page>`_ (Out of date)


Plugins
-------

* `Writing plugins with Grunt <https://github.com/NodeBB-Community/nodebb-grunt>`_
* `Writing your first NodeBB plugin <http://burnaftercompiling.com/nodebb/writing-your-first-nodebb-plugin/>`_


Themes
------

Widgets
-------

Debugging 
-------
(Linux and OSX)

* Install node-inspector from npm: ``npm i node-inspector -g``

* Start NodeBB in development mode: (in NodeBB root dir): ``./nodebb dev``

  * This starts up only one fork so you don't get the ``EADDRINUSE`` error

* In a new terminal, run ``node-inspector &`` (spins up as a background process, so if something goes wrong, use ``ps aux | grep node-inspector`` to find the pid and kill it)

This will output something like:

.. code::

    Visit http://127.0.0.1:8080/debug?ws=127.0.0.1:8080&port=5858 to start debugging.

* Press enter to get back to the command line

* Type ``ps aux | grep app.js`` to see:

.. code::

    brian           79177   0.0  0.0  2432772    660 s006  R+   10:03PM   0:00.00 grep app.js
    brian           79089   0.0  1.1  3763608 183804 s005  S+    9:41PM   0:04.91 /usr/local/Cellar/node/0.12.5/bin/node app.js

* The pid for NodeBB is 79089 in this case, so just type the command ``kill -s USR1 79089`` and you should see this in the terminal where you spun up ./nodebb dev:

.. code::

    Starting debugger agent.
    Debugger listening on port 5858

* Go load the address you got from node-inspector in your browser ^ (it might take a second to load)

* Set a breakpoint somewhere (that you know how to hit) and you should be up and running!

* Now you can also just ctrl-C to quit the NodeBB process. When you want to start it again:

* Start ./nodebb dev again
* Use ``ps aux | grep app.js`` to find the pid again
* Since node-inspector is still running in the background, you just have to send a ``kill -s USR1 <pid>`` to the new pid of the running nodebb instance, and refresh the browser window that had the debugger open originally

Troubleshooting
^^^^^^^^^^^^^^^^^^

**I still get the EADDRINUSE error**

* Upgrade to node 0.12.5 (0.12.x should be sufficient)

* If you had already installed node-inspector and NodeBB prior to upgrading to node 0.12.x, you'll have to rebuild your node packages:

  * In your NodeBB root directory, run ``npm rebuild``
  * In your node-inspector root dir, also run ``npm rebuild``
    * If you nstalled node-inspector through npm (``npm install -g node-inspector``), go to ``/usr/local/lib/node_modules/node_inspector`` and run ``npm rebuild``
