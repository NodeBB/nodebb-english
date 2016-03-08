Openshift PaaS
===========

**Notice: ** A quickstart has been made to handle much of the below by using openshift's environment variables. If you're just getting started please take a look at <a href="https://github.com/ahwayakchih/openshift-nodebb" target="_blank">https://github.com/ahwayakchih/openshift-nodebb</a>

The following are installation instructions for the `Openshift <http://openshift.com>` PaaS. Before starting, you need to install Red Hat's rhc command line at <a href="https://developers.openshift.com/en/managing-client-tools.html" target="_blank">https://developers.openshift.com/en/managing-client-tools.html</a>

**Step 1:** Go to <a href="https://openshift.redhat.com/app/console/applications" target="_blank">https://openshift.redhat.com/app/console/applications</a> and then create an application.

**Step 2:** Scroll down and choose Node.js 0.10 in "Other types". Then click 'Next'.

**Step 3:** Type `nodebb` in application name. If you want another name, you might want this instead: `nodebb-(name)`. Replace `(name)` to whatever you like.
Note: If it's your first time, you will see a note saying you need to specify a namespace. Namespace can be anything ... as long you do not change application name.

**Step 4:** Scroll all the way down and click 'Create Application'. Then you need to wait for it to finish creating your first NodeBB application.
Note: Do not make any changes to your application, just leave them as it is. Otherwise do it at your own risk as NodeBB might will not work correctly.

**Step 5:** You will be asked if you want to code your application. Simply click 'Not now, contiune'. Then you will be redirected to an application page. It will tell you that it is created without any errors and it is started.

**Step 6:** Click 'see the list of cartridges you can add'. Choose the MongoDB cartridge. Then click 'Next'. You should see if you want to confirm. Click 'Add Cartridge'.

**Step 7:** You should see the notice that it is installed without any errors. It also will tell you the credentials you need to use to access it. Write it down somewhere, as you will need it later.

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
echo $OPENSHIFT_NODEJS_IP && echo $OPENSHIFT_MONGODB_DB_HOST && echo $OPENSHIFT_MONGODB_DB_PORT
```

In order:
First line: NodeJS IP address - You should save it.
Second line: Mongodb IP address - Write it down.
Third line: Mongodb Port - Write it down.

**Step 10:** Exit SSH by pasting the following command.
```
exit
```

Note: You might have to type 'exit' once, and then again to exit SSH completely.

**Step 11:** Go back to <a href="https://openshift.redhat.com/app/console/applications" target="_blank">https://openshift.redhat.com/app/console/applications</a> and then click NodeBB application. Copy the URL address from "Scoure Code."
A similar scoure code URL address should be this: ssh://[code]@nodebb-[namespace].rhcloud.com/~/git/nodebb.git/

**Step 12:** Go back to terminal. Paste the following command and then paste the URL address.
```
git clone ssh://[code]@nodebb-[namespace].rhcloud.com/~/git/nodebb.git/
```

Note: If it exists, check to make sure you do not have more than four files. If it is, delete it and rerun the command. Otherwise contiune to next step.

Note: This will create NodeBB folder on your computer, usually ~/users/[name]/NodeBB

**Step 13:** Then cd to NodeBB folder on your computer. And you will need to clone NodeBB from Github to your application by using this command. The default command git clone will not work with Openshift, unless you're in SSH. You may split up this command into two parts if you needed to clone your repository to another part of your computer start git bash from there.
```
cd nodebb && git remote add upstream -m master https://github.com/NodeBB/NodeBB.git
or
cd nodebb
git remote add upstream -m master https://github.com/NodeBB/NodeBB.git
```

**Step 14:** Then pull files from NodeBB's repository.
```
git pull -s recursive -X theirs upstream v1.x.x
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

*URL used to access this NodeBB (http://localhost:4567)* - Copy and paste your application's URL address and then add port 8080 like so: http://nodebb-[namespace].rhcloud.com:8080

*Please enter a NodeBB secret (code)* - Just press enter.

*Which database to use (redis)* - enter `mongo`.

*Host IP or address of your Mongo instance (127.0.0.1)* - Copy & paste Mongo's IP address found in step 9.

*Host port of your Mongo instance (6379)* - Copy & paste Mongo's port found in step 9.

*Password of your Mongo database* - Enter your Mongo password found in step 7 or step 9.

*Which database to use (0)* - Enter the database name you got in step 7.

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
