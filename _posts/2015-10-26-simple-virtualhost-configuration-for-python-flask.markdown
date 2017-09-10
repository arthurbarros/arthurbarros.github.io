---
published: true
title: Simple VirtualHost configuration for Python Flask
layout: post
author: Arthur Barros
header-img: "img/2015-10-26-simple-virtualhost-configuration-for-python-flask.jpg"
---
During this whole year, I've been involved in several web app using Flask, and several vhost configuration type. 

The most problematic one was the WSGIDaemon, wich lets Apache to fireup N daemon of you application, this approach could lead for a database issues (which did).
A quick google will show for some cases  -- [stackoverflow](http://stackoverflow.com/questions/9318347/why-are-some-mysql-connections-selecting-old-data-the-mysql-database-after-a-del)

The following is currently the one who fits my needs


    <VirtualHost *:80>
            ServerName my_awesome_site.com.br

            WSGIScriptAlias / /path/to/app/application.wsgi
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
