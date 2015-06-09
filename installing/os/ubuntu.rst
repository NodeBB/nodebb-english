
Ubuntu
--------------------

First, we install our base software stack:

.. code:: bash

	$ sudo apt-get install git nodejs nodejs-legacy npm redis-server imagemagick build-essential


If you want to use MongoDB, LevelDB, or another database instead of Redis please look at the :doc:`Configuring Databases <../../configuring/databases>` section.

**If your package manager only installed a version of Node.js that is less than 0.8 (e.g. Ubuntu 12.10, 13.04), use ``node --version`` to determine your version of Node.js:**


.. code:: bash

	$ sudo add-apt-repository ppa:chris-lea/node.js
	$ sudo apt-get update && sudo apt-get dist-upgrade

If you'd like to install Node.js v0.11, use the repository url ``ppa:chris-lea/node.js-devel`` instead.
The npm is installed with the nodejs

Next, clone this repository:


.. code:: bash

	$ git clone -b v0.7.x https://github.com/NodeBB/NodeBB.git nodebb


Obtain all of the dependencies required by NodeBB:

.. code:: bash

    $ cd nodebb
    $ npm install --production


Start the NodeBB Web Installer, and continue setup at http://127.0.0.1:4567.

.. code:: bash

    $ npm start

----

**Alternatively**: Initiate the setup script by running the app with the ``setup`` flag:


.. code:: bash

	$ ./nodebb setup


The default settings are for a local server running on the default port, with a redis store on the same machine/port. 

Lastly, we run the forum.


.. code:: bash

	$ ./nodebb start


NodeBB can also be started with helper programs, such as ``forever``. :doc:`Take a look at the options here <../../running/index>`.
