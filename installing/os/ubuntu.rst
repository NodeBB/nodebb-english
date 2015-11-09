
Ubuntu
--------------------

The following installation guide is optimised for Ubuntu LTS versions, and will install NodeBB
with MongoDB as the data store. Currently at the time of writing, the latest available Ubuntu
LTS version is **14.04**.

----

First, install the LTS version of Node.js (**v4.2 Argon**):

.. code:: bash

	$ curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -

Next, we'll install the dependencies required by NodeBB

.. code:: bash

	$ sudo apt-get install -y git nodejs mongodb build-essential


If you want to use Redis or another database instead of MongoDB please look at the :doc:`Configuring Databases <../../configuring/databases>` section.

Next, clone NodeBB into your desired location. If you don't know where, your home directory is acceptable:


.. code:: bash

	$ cd ~   # Optional
	$ git clone -b v0.9.x https://github.com/NodeBB/NodeBB.git nodebb


Obtain all of the dependencies required by NodeBB:

.. code:: bash

    $ cd nodebb
    $ npm install --production


Start the NodeBB Web Installer, and continue setup at http://127.0.0.1:4567, and select "MongoDB"
as your database type.

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

----

If you receive an error stating ``Error: Cannot find module '../build/Release/magic'``, run ``npm i mmmagic``
and continue as before.