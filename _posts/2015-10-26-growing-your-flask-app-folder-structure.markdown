---
published: true
title: Growing your Flask App - Folder Structure
layout: post
header-img: "img/post-bg-01.jpg"
---

Flask is pretty straightforward while reading and learning the basics of the framework. But as soon as your needs start to grow you face a challenge of how to proper grow and organize your Models, Views and Controllers.

The following is the result of trial-and-error during several projects using Flask + Blueprints + SQLAlchemy

## Structure

     app_name/
     - - shared/
     - - - - __init__.py
     - - - - helpers.py
     - - - - models.py
     - - webapp/
     - - - - modules/
     - - - - __init__.py
     - - - - - - auth/
     - - - - - - - - templates/
     - - - - - - - - - - login.html
     - - - - - - - - controller.py
     - - - - - - - - model.py
     - - - - - - - - form.py
     - - - - - - - - routes.py
     - - - - - - - - __init__.py
     - - - - - - home/
     - - - - - - - - templates/
     - - - - - - - - - - index.html
     - - - - - - - - controller.py
     - - - - - - - - model.py
     - - - - - - - - form.py
     - - - - - - - - routes.py
     - - - - - - - - __init__.py
     - - - - - - [ . . . ]
     - - - - static/
     - - - - - - css/
     - - - - - - js/
     - - - - - - images/
     - - - - templates/
     - - - - - - layout.html
     - - - - webapp.wsgi
     - - - - config.py
     - - - - __init__.py
     - - webadmin/
     - - - - < same of webapp >
     - - run_app.py
     - - run_admin.py
     - - __init__.py
 

## So what any of this mean?

The example above is straightforward, but I will enlighten some of those paths.

`app_name/shared/` This folder is the collection of everything you can share between you front-office and back-office application, such as common models that will be used in the whole application, Abstract objects for you SQLAlchemy models for example.

` app_name/webapp/modules/<module_name>/model.py` Is used to built specific Business Logic releated only to that module.

` app_name/webapp/templates/*.html` If you have an html whiche is used by different modules such as the layout who is injected in each html view (using JINJA2 extends for example).

` app_name/webapp/webapp.wsgi` This is the entrypoint for your wsgi server, such as Apache2 WSGIScriptAlias flag

`app_name/run_*.py` is a little tweak to run the development ambient, the internal flask web-server without having to configure a local nginx/Apache for your project


With this structure I have satisfied almost any need for common web application I've encountered so far. 
This isn't a silver-bullet solution because every problem should be studied and see what solution fits best. 
Any how this solution can satisfy most small/medium web apps with a simple  architecture stack
 
