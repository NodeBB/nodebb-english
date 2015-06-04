NodeBB & Redis Installation
===========

Requirements
---------------

In order to use the NodeBB Docker builds, you will need to have Docker installed. You can find install instructions
for your system at `http://docs.docker.com/ <http://docs.docker.com/>`_.

Stable/Development Builds
---------------

By default, the NodeBB Docker builds install the stable version of NodeBB. To install the development version of
NodeBB, simply append dev to the commands `-dev`. 

Usage
---------------

To get started with running NodeBB using Docker, you will want to run a redis instance.

.. code:: bash

    docker run --name my-forum-redis -d -p 6379:6379 nodebb/docker:centos-redis
    docker run --name my-forum-redis -d -p 6379:6379 nodebb/docker:ubuntu-redis

Next, launch the NodeBB instance, so it links with the just-launched Redis instance.

.. code:: bash

    docker run --name my-forum-nodebb --link my-forum-redis:redis -p 80:80 -p 443:443 -p 4567:4567 -P -t -i nodebb/docker:centos

.. code:: bash

    docker run --name my-forum-nodebb --link my-forum-redis:redis -p 80:80 -p 443:443 -p 4567:4567 -P -t -i nodebb/docker:ubuntu 

You will be asked to configure your NodeBB instance, as no config file was found. Simply press enter for all settings 
except Redis hostname, which should be `redis` as it is linked using the `--linked` parameter to our Redis instance, 
and the administrator username, e-mail and password. 

The default port of nodebb is 4567. Ports 80, and 443 have also been exposed for your convenience. You can keep the 
default nodebb port or change it.

NodeBB will launch the setup and automatically close. Next, simply start the instance again. It will this time 
find a config file and start as a daemon.

.. code:: bash

    docker start my-forum-nodebb

Your NodeBB instance will be accessible on the port you selected during setup. Check `docker ps` for more details.

Backup/Restoring
---------------

Simply use the `/data` volume inside your Redis instance. See 
the `official guide on making backups <https://docs.docker.com/userguide/dockervolumes/#backup-restore-or-migrate-data-volumes)>`_.

