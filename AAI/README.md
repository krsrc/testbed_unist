# AAI - INDIGO IAM

## Requirements
- firewall (ex.ufw,firewalld)
- snap
- if necessary, private certificates

## Installation
### STEP1. set up proxy server   

- install NGINX   
```
$ sudo apt install nginx
```

- allow NGINX at firewall
> [!NOTE]   
> case of ufw
```
$ sudo ufw app list
Available applications:
Nginx Full
Nginx HTTP
Nginx HTTPS

$ sudo ufw allow 'Nginx HTTP'
Rule added
Rule added (v6)

$ sudo ufw status
Status: active

To                 Action        From
---                -------       ------
Nginx HTTP         ALLOW         Anywhere
Nginx HTTP (v6)    ALLOW         Anywhere (v6)
```

- check NGINX status   
```
$ sudo systemctl status nginx
nginx.service - A high performanc web server and a reverse proxy server
Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
Active: active (running) since XXX 2023-XX-XX XX:XX:XX KST; XXmin ago
Docs: man:nginx(8)
Process: XXXXX ExecStartPre=/usr/sbin/nginx -t -q -g daemon on; master_process on; (code=existed, status=0/SUCCESS)
Process: XXXXX ExecStart=/usr/sbin/nginx -g daemon on; master_process on; (code=existed, status=0/SUCCESS)
Main PID: XXXXX (nginx)
Tasks: 65 (limit: 154443)
Memory: 49.1M
CPU: 533ms
CGroup: /system.slice/nginx.service
      ⨽25447 "nginx: master process /usr/sbin/nginx -g daemon on; master_process on;"
      ⨽25449 "nginx: worker process" ""  ""  ""  ""  ""  ""  ""  ""  ""  ""  ""  ""  ""  ""  ""  ""  ""  ""  ""  ""  ""  ""  ""  ""  ""  ""  "" 
```

- check NGINX on the browser   
  - find localhost (XX.XX.XX.XX)
  - http://localhost on the web browser
 ![image](https://github.com/krsrc/testbed_unist/assets/139738228/d74a2b6f-4e6b-49bf-8bf7-14f5a889ac75)


### STEP2. certificates   
- install snap   
```
$ sudo snap install core; sudo snap refresh core
[sudo] password for hslee:
core XX-XX.XX.XX from Canonical✓ installed
snap "core" has no updates available
```

- remove old version of cerbot   
```
$ sudo apt remove certbot
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Package 'certbot' is not installed, so not removed
0 upgraded, 0 newly installed, 0 to remove and 18 not upgraded.
```

- install cerbot   
```
$ sudo snap install --classic certbot
certbot 2.6.0 from Certbot Project (certbot-eff✓) installed
```

- address link   
```
$ sudo ln -s PATH_WHERE_CERBOT_IS_LOCATED_UNDER_SNAP_DIRECTORY PATH_LOCAL_DIRECTORY_WHERE_INSTALLED_SOFTWARES_ARE_LOCATED
```

- allow HTTPS   
```
$ sudo ufw allow 'Nginx Full'
$ sudo ufw delete allow 'Nginx HTTP'
```

> [!NOTE]
> skip intermediate steps for generating certificates when using private ones.

- stop NGINX   
```
$ sudo systemctl stop nginx
```

- modify NGINX configuration file   
```
$ sudo vi /etc/nginx/sites-available/defualt
```   

<pre>
server {
  listen        443 ssl;
  server_name   <b>Your_HOSTNAME_Here</b>;
  access_log    /var/log/nginx/iam.access.log combined;

  ssl_on;
  ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
  ssl_certificate      <b>/PATH_TO_YOUR_SSL/</b>cert.pem;
  ssl_certificate_key  <b>/PATH_TO_YOUR_SSL/</b>key.pem;

  location / {
    proxy_pass              http://<b>THE_IAM_APP_HOSTNAME_HERE</b>:8080;
    proxy_set_header        X-Real-IP $remote_addr;
    proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header        X-Forwarded-Proto https;
    proxy_set_header        Host $http_host;
  }
}
</pre>

- restart NGINX
```
$ sudo systemctl restart nginx
```

### STEP3. Database   
- install MariaDB
```
$ sudo apt install mariadb-server
```

- configure MariaDB
```
$ sudo mysql_secure_installation
```



### STEP4. JSON Web Keys

### STEP5. INDIGO IAM


## Link
[INDIGO IAM](https://indigo-iam.github.io/v/v1.8.2/docs/getting-started/)   
[MariaDB v.11.2](https://mariadb.com/kb/en/changes-improvements-in-mariadb-11-2/)   
[MySQL v.8.0](https://dev.mysql.com/doc/mysql-installation-excerpt/8.0/en/linux-installation.html)   
[JSON Web Keys](https://github.com/bspk/json-web-key-generator)   
[SSL certificates](https://deoking.tistory.com/7)   
