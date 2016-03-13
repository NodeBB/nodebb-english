
Arch Linux
--------------------

First, we install our base software stack.  Be sure to `pacman -Syu` first to make sure you've synced with the repositories and all other packages are up to date.

.. code:: bash

	$ sudo pacman -S git nodejs npm redis imagemagick


If you want to use MongoDB, LevelDB, or another database instead of Redis please look at the :doc:`Configuring Databases <../../configuring/databases>` section.

Next, clone this repository:


.. code:: bash

	$ git clone -b v1.0.0 https://github.com/NodeBB/NodeBB.git nodebb

You'll want to replace ``v1.0.0`` with the (`latest stable version <https://github.com/NodeBB/NodeBB/releases>`_), or ``v1.x.x`` if you'd like
to set up the latest weekly build of NodeBB.

Obtain all of the dependencies required by NodeBB:

.. code:: bash

    $ cd nodebb
    $ npm install


Initiate the setup script by running the app with the ``setup`` flag:


.. code:: bash

	$ ./nodebb setup


The default settings are for a local server running on the default port, with a redis store on the same machine/port.

Lastly, we run the forum.


.. code:: bash

	$ ./nodebb start


NodeBB can also be started with helper programs, such as ``supervisor`` and ``forever``. :doc:`Take a look at the options here <../../running/index>`.
