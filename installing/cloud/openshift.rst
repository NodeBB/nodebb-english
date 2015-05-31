Openshift PaaS
===========

The following are installation instructions for the `Openshift <http://openshift.com>` PaaS. Before starting, you need to install Red Hat's rhc command line at https://developers.openshift.com/en/managing-client-tools.html.

**Step 1:** Go to https://openshift.redhat.com/app/console/applications and then create an application.

**Step 2:** Scroll down and paste the following URL address in "Code Anything" field box. Then click 'Next'.
```
http://cartreflect-claytondev.rhcloud.com/github/icflorescu/openshift-cartridge-nodejs
```

**Step 3:** Type `nodebb` in application name. If you want another name, you might want this instead: `nodeb-(name)`. Replace `(name)` to whatever you like.
Note: If it's your first time, you will see a note saying you need to specify a namespace. Namespace can be anything ... as long you do not change application name.

**Step 4:** Scroll all the way down and click 'Create Application'. Then you need to wait for it to finish creating your first NodeBB application.
Note: Do not make any changes to your application, just leave them as it is. Otherwise do it at your own risk as NodeBB might will not work correctly.

**Step 5:** You will be asked if you want to code your application. Simply click 'Not now, contiune'. Then you will be redirected to an application page. It will tell you that it is created without any errors and it is started.

**Step 6:** Click 'see the list of cartridges you can add'. Scroll down and then past the following URL address to "Install your own cartridge" field box. Then click 'Next'. You should see if you want to confirm. Click 'Add Cartridge'.
```
http://cartreflect-claytondev.rhcloud.com/reflect?github=smarterclayton/openshift-redis-cart
```

**Step 7:** You should see the notice that it is installed without any errors. It also will tell you the default password. Save it somewhere, as you will need it later.

**Step 9:** Open terminal (or Git Bash) and paste the following command to access SSH.
```
rhc app ssh -a nodebb
```

Note: If you got an error that it does not exist or similar, you need to do the following command and then try again.
```
rhc setup
```

**Step 9:** Paste the following command. Then save the necessary information.
```
echo $OPENSHIFT_NODEJS_IP && echo $REDIS_CLI
```

In order:
First line: NodeJS IP address - You should save it.
Second line: Redis IP address `-h` - You should save it. Redis Port `-p` - You should save it. Redis Password `-a` - It was already explained in Step 7.

Note: If you're installing NodeBB with Redis first time, you should wipe databases (or one of your choice). Paste the following code.
```
redis-cli $REDIS_CLI
```
then
```
flushall
```
or
```
select db_number_of_your_choice
flushdb
```

**Step 10:** Exit SSH by pasting the following command.
```
exit
```

Note: You might have to type 'exit' once, and then again to exit SSH completely.

**Step 11:** Go back to https://openshift.redhat.com/app/console/applications and then click NodeBB application. Copy the URL address from "Scoure Code."
A similar scoure code URL address should be this: ssh://[code]@nodebb-[namespace].rhcloud.com/~/git/nodebb.git/

**Step 12:** Go back to terminal. Paste the following command and then paste the URL address.
```
git clone ssh://[code]@nodebb-[namespace].rhcloud.com/~/git/nodebb.git/
```

Note: If it exists, check to make sure you do not have more than four files. If it is, delete it and rerun the command. Otherwise contiune to next step.

Note: This will create NodeBB folder on your computer, usually ~/users/[name]/NodeBB

**Step 13:** Then cd to NodeBB folder on your computer. And you will need to clone NodeBB from Github to your application by using this command. The default command git clone will not work with Openshift, unless you're in SSH.
```
cd nodebb && git remote add upstream -m master https://github.com/NodeBB/NodeBB.git
```

**Step 14:** Then pull files from NodeBB's repository.
```
git pull -s recursive -X theirs upstream v0.7.x
```

**Step 15:** Now you will need to commit and push files to your application's repository. Replace `message` with your message. It will take a while to finish, though.
```
git commit -a -m 'message' && git push
```

**Step 16:** Access SSH again.
```
rhc app ssh -a nodebb
```

**Step 17:** First `cd` then start the installation of NodeBB using interactive installer.
```
cd ~/app-root/repo && ./nodebb setup
```

Note: Web installer (npm start) might will not work because... it's Openshift.

**Step 18:** Follow what this step carefully!!!

*URL used to access this NodeBB (http://localhost:4567)* - Copy and paste your application's URL address and then add port 8080 like so: http://nodeb-[namespace].rhcloud.com:8080

*Please enter a NodeBB secret (code)* - Just press enter.

*Which database to use (redis)* - Database of your choice, otherwise just press enter.

*Host IP or address of your Redis instance (127.0.0.1)* - Copy & paste Redis' IP address found in step 9.

*Host port of your Redis instance (6379)* - Copy & paste: 16379 OR copy & paste Redis' port found in step 9.

*Password of your Redis database* - Enter your Redis password found in step 7 or step 9.

*Which database to use (0)* - Just press enter, unless you perfer different database, go ahead.

**Step 19:** Now you will need to edit config.json NodeBB had created. Paste the following command.
```
nano config.json
```

**Step 20:** Add a line below "url" and then add the following. Repleace NodeJS IP Address to IP address of your application found in step 9. Then exit the editor using CTRL+X.
```
"bind_address": "NodeJS IP Address",
```

**Step 21:** Now start your NodeBB on Openshift! And you're done! Then visit your website: http://nodebb-[namespace].rhcloud.com/
```
./nodebb start
```

Note
---------------------------------------
Starting, stopping, reloading, or restarting NodeBB now works on Openshift. Be sure you always do this before doing it. (Replace `[string]` to a valid string.)

.. code:: bash
	
	rhc app ssh -a nodebb
    cd ~/app-root/repo
    ./nodebb [string]
