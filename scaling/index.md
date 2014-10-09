# Scaling NodeBB

When it comes to maintaining many concurrent connections or high view rates, there are certain procedures that can be followed in order to streamline NodeBB.

This article attempts to outline the various strategies that can be employed by those finding that NodeBB is not running as fast as it should under full load.


## Utilise clustering

By default, NodeBB will run on one process, and certain calls may take longer than others, resulting in a lag or queue for the same resources. To combat this, you can instruct NodeBB to run on multiple processes:

`./nodebb start --cluster`

By default, NodeBB will detect the number of virtual cores on the system and start that many processes. To only start a specific number:

`./nodebb start --cluster=2`

If you do not wish to pass the `--cluster` flag every time you start NodeBB, you can also add the `cluster` property into your `config.json`.


## Use a proxy server to serve static assets

Nginx is exceedingly good at serving static resources (e.g. javascript, css, images, etc). By allowing Nginx to take over the task of serving this to the end user, the NodeBB process(es) will be left to handle only the API calls, which substantially lowers the amount of work for NodeBB (and increases your throughput).

Your Nginx config will need to be modified to look something like this:

    server {
        listen 80;

        server_name community.nodebb.org;

        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_set_header X-NginX-Proxy true;
        proxy_redirect off;

        # Socket.io Support
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";

        gzip            on;
        gzip_min_length 1000;
        gzip_proxied    off;
        gzip_types      text/plain application/xml application/x-javascript text/css application/json;

        location @nodebb {
            proxy_pass http://127.0.0.1:4567;
        }

        location ~ ^/(images|language|sounds|templates|uploads|vendor|src\/modules|nodebb\.min\.js(\.map)?|stylesheet\.css|admin\.css) {
            root /path/to/nodebb/public/;
            try_files $uri $uri/ @nodebb;
        }

        location / {
            proxy_pass http://127.0.0.1:4567/;
        }
    }