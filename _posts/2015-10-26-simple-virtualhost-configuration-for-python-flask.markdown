---
published: false
title: Simple VirtualHost configuration for Python Flask
layout: post
---
I've been a PHP developer for a long time, but a year from now I started digging into Python -- specifically in flask micro-framework.

During this whole year, I've been involved in several web app using Flask, and several vhost configuration type. The most problematic one was the WSGIDaemon, wich let's Apache to fireup N daemon of you application, this approach could lead for a database issues (which did).
A quick google will lead for some cases  -- [stackoverflow](http://stackoverflow.com/questions/9318347/why-are-some-mysql-connections-selecting-old-data-the-mysql-database-after-a-del)

```
<VirtualHost *:80>
        ServerName cambo.com.br

        WSGIScriptAlias / /var/www/cambo/cambo.wsgi
        <Directory /path/to/app/>
            Order allow,deny
            Allow from all
        </Directory>
        Alias /static /path/to/app/static
        <Directory /path/to/app/static/>
            Order allow,deny
            Allow from all
        </Directory>

        ErrorLog ${APACHE_LOG_DIR}/error.log
        LogLevel warn
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
``` 