The NodeBB Config (``config.json``)
===================================

The majority of NodeBB's configuration is handled by the Administrator
Control Panel (ACP), although a handful of server-related options are
defined in the configuration file (``config.json``) located at NodeBB's
root folder.

Some of these values are saved via the setup script:

-  ``url`` is the full web-accessible address that points to your
   NodeBB. If you don't have a domain, an IP address will work fine
   (e.g. ``http://127.0.0.1:4567``). Subfolder installations also define
   their folder here as well (e.g. ``http://127.0.0.1:4567/forum``)
-  ``secret`` is a text string used to hash cookie sessions. If the
   secret is changed, all existing sessons will no longer validate and
   users will need to log in again.
-  ``database`` defines the primary database used by NodeBB. (e.g.
   ``redis`` or ``mongo``) -- for more information, see :doc:`Configuring Databases <databases>`
-  Both ``redis`` and ``mongo`` are hashes that contain database-related
   connection information, they contain some or all of the following:

   -  ``host``
   -  ``port``
   -  ``username`` (MongoDB only)
   -  ``password``
   -  ``database``

The following values are optional, and override the defaults set by
NodeBB:

-  ``port`` (Default: ``4567``) Specifies the port number that NodeBB
   will bind to. You can specify an array of ports and NodeBB will spawn port.length processes. 
   If you use multiple ports you need to configure a load balancer to proxy requests to the different ports.
   
-  ``bcrypt_rounds`` (Default: 12) Specifies the number of rounds to
   hash a password. Slower machines may elect to reduce the number of
   rounds to speed up the login process, but you'd more likely want to
   *increase* the number of rounds at some point if computer processing
   power gets so fast that the default # of rounds isn't high enough of
   a barrier to password cracking.
-  ``upload_path`` (Default: ``/public/uploads``) Specifies the path,
   relative to the NodeBB root install, that uploaded files will be
   saved in.
   
- ``jobsDisabled`` This can be added to disable jobs that are run on a certain interval. For example "jobsDisabled":true will disable daily digest emails and notification pruning.

- ``socketio`` A hash with socket.io settings :

   - ``transports`` (Default: ``["polling", "websocket"]``) Can be used to configure socket.io transports.
   - ``address`` (Default: ``""``) Address of socket.io server can be empty






