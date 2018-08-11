Digitalocean Account and Payment Setup

Digitalocean Server 5 Dollar Ubuntu 18.04

Inital Setup
	https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-18-04
	Note : Keep firewall ports 22, 80, 443 and 19999 open

Install pip, virtualenv

Create a virtual env, Clone contribook, Install requirements.txt and Build

Install Nginx, Setup Server Block in Nginx Config and Restart Nginx
```
server {
        listen 80;
        server_name <INSERT IP HERE>;

        location = /favicon.ico { access_log off; log_not_found off; }

        location = / {
                return 302 http://<INSERT IP HERE>/contribook/;
        }

        location /contribook {
                alias /home/raghuram/contribook/contribook/_build/html;
                index index.html;
                try_files $uri $uri/ =404;
        }
}
```


Install Netdata

Set up HTTPS using Lets Encrypt

Set up Domain Name



