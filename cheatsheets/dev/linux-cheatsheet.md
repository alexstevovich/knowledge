### General Notes
Putty seems like a good console ap to console. Right Click on mouse is usually the default setting to paste in Putty.

Filezilla is good to manage the file system visually.


# Super User
```sh
echo "Enter the super username:"
read USER_NAME
adduser $USER_NAME
usermod -aG sudo $USER_NAME
```
# Firewall
```sh
ufw app list
ufw allow OpenSSH
ufw enable -y
ufw status
```

# NGINX
```sh
sudo apt install nginx -y
#Weird hack to bypass an issue on ubuntu22
sudo apt-get remove nginx
sudo apt update
sudo apt install nginx
#should show nginx http here:
sudo ufw app list
```

## NGINX Firewall
```sh
sudo ufw allow 'Nginx Full'
sudo ufw enable -y
systemctl status nginx
```

## NGINX Registration


### Reverse Proxy Example

A standard example of a reverse proxy. Replace the server_name websites and also the proxy_pass PORT to use whatever port your webapp listens for.


default.nginxconf
``` 
server {
    listen 80;
    server_name my-website.com www.my-website.com;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        
        # Forward client-related information
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Forwarded-Host $host;
        proxy_set_header X-Forwarded-Port $server_port;
        proxy_set_header X-Forwarded-Server $host;
        
        proxy_cache_bypass $http_upgrade;
    }
}
```
I use the ext: nginxconf so i can identify what kind of file it is compared to extensionless default or the often seen .conf. Add one of these files for each webapp you are using and call the file name an id for the webapp that is using the port:

**Example:** mywebpp.nfginxconf



### Commands

```sh
sudo ln -s /etc/nginx/sites-available/CONFIGFILE /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

Config file can be named anything included the extension. I use .nginxcfg

# HTTPS 
Do this after Nginx

``` sh
sudo apt install -y certbot python3-certbot-nginx
sudo certbot --nginx --register-unsafely-without-email -d site1.com -d www.site1.com
```

Register all domains that you must use https here. Note the regular + www. variations.  You can provide an email but it's publicly visible. You can live "dangerously" with the '--register-unsafely-without-email' arg.

# Normal commands

## Install Programs 
``` sh
apt-get install -y nodejs
apt-get install -y npm
```

## Make Symlink
make a symlink to a file
``` sh
ln -s /INPUT_PATH/INPUT_FILENAME /OUTPUT_PATH/

#wildcard variation
ln -s /INPUT_PATH/INPUT_FILENAME/* /OUTPUT_PATH/
```

# Services

## Template

here is an example using a nodejs webapp that listens to a port:

example.service
```
[Unit]
Description=my_webapp_description
After=network.target

[Service]
Type=simple
User=root
WorkingDirectory=/path/to/webapp/
ExecStart=/usr/bin/node /path/to/webapp/index.js
Restart=always
RestartSec=10
Environment=NODE_ENV=production
Environment="PORT=3000"

[Install]
WantedBy=multi-user.target
```
* my_webapp_description can be whatever you want
* You can pass as many environment vars as needed. In this example i pass the port i want the webapp to use
* I'm starting with an index.js file but you can trigger this however you want.

## Place the service files.
Create a symlink from your service file to the /etc/systemd/system directory. Ensure the .service extension is used on the file.

## Commands to interact with the services:
``` sh
sudo systemctl daemon-reload
sudo systemctl enable SERVICE_WITHOUT_EXT
sudo systemctl start SERVICE_WITHOUT_EXT
sudo systemctl restart SERVICE_WITHOUT_EXT
systemctl status service-name
```

**SERVICE_WITHOUT_EXT:** Means you take the filename and write it without it's extension.

If your settings allow it, these will also restart the service if the system restarts.