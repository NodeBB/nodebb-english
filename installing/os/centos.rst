
CentOS 6/7
--------------------

First we should make sure that CentOS is up to date, we can to so using this command:

.. code:: bash
	
	yum -y update

**If your on CentOS 7, you will need to install the epel release, you can do so using the following command:

.. code:: bash
	
	yum -y install epel-release
	

Now, we install our base software stack:

.. code:: bash

	yum -y groupinstall "Development Tools"
	yum -y install nodejs git redis ImageMagick npm

If you want to use MongoDB, LevelDB, or another database instead of Redis please look at the :doc:`Configuring Databases <../../configuring/databases>` section.

Next, clone the NodeBB repository:

.. code:: bash

	cd /path/to/nodebb/install/location
	git clone -b v0.7.x https://github.com/NodeBB/NodeBB nodebb
	
**Note: To clone the master branch you can use the same command with out the "-b" option.

After cloning the repository, obtain all of the dependencies required by NodeBB:

.. code:: bash
      
      cd nodebb
      npm install

Initiate the setup script by running the app with the ``setup`` flag:

.. code:: bash

	  ./nodebb setup


The default settings are for a local server running on the default port, with a redis store on the same machine/port. 

Lastly, we run the forum.
  
.. code:: bash

	 ./nodebb start

NodeBB can also be started with helper programs, such as ``forever``. :doc:`Take a look at the options here <../../running/index>`.
