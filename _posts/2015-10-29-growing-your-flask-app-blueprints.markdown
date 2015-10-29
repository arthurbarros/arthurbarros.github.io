---
published: true
title: Growing your Flask App - Blueprints
layout: post
---

_If you didn't read the previous post about this topic, please go ahead to [Growing your Flask App - Folder Structure](http://arthurbarros.github.io/2015/10/26/growing-your-flask-app-folder-structure.html)_

The simplest way I found so far to organize my Flask apps is to using the [HMVC](https://en.wikipedia.org/wiki/Hierarchical_model%E2%80%93view%E2%80%93controller) pattern.
The concept is really easy to get used to, but it can be trick to implement with your Flask application because of the poor *official* documentation.

## Mapping the modules folder

Refactor your `__init__.py` at the root of your app, and use the register_blueprint which is builtin to the `flask.blueprint` object.

`app_name/webapp/__init__.py`


     from flask import Flask
     import modules.home.routes
     app = Flask(__name__)
     app.register_blueprint(modules.home.routes.blueprint)


Everytime we create a new module we have to import it and register the Blueprint object to the app instance. So our application become aware of the new module.

## Mapping our routes to the module controller's a.k.a routes.py

Each of our modules should have a mandatory routes.py file, responsible to map each route of your app to the matching controller.
To solve it we are going to import our module controller relative to our routes.py and than initiate a new Blueprint instance.

`app_name/webapp/modules/home/routes.py`
     
     from flask import Blueprint
     import controller
     blueprint = Blueprint("home", __name__, url_prefix='/', template_folder='templates')
     blueprint.route("/", methods=["GET"])(controller.index)
     

At the 4th line, we are creating a new instance of the Blueprint class, the first argument, is the module name which we are going to use when referencing our modules using the [url_for()](http://flask.pocoo.org/docs/0.10/api/#flask.url_for) method.

`url_prefix` is used to proper name your modules to the url, for example `url_prefix='account'`
 would give us the following url path to our module http://url/account/<controller
 
 `template_folder` it takes the relative path to the `routes.py` file to look for our templates we are going to use with the controller we assined to. Everytime our `controller.index` method tries to resolve a template to render with `render_temaplte`method it will look this to the `teamplte_folder` path under our module, and if it don't find any matching file it will look at the `app_name/webapp/templates` for a matching. 
 
 _Be aware with you have multiple template files with the same name under different modules it WILL resolve the first one it finds, no matter what module it is, this is a known issue by the time i write this post_

At the 5th line, we are assinging our routes with the proper http method it handle to the method reponsible to solve it.

`blueprint.route` the first argument is the name will be assigned to the controller method, for example `blueprint.route("magic_the_gathering, methods=["GET"])(controller.index)"` will result in the following uri http://url/account/magic_the_gathering

## Conclusion

With this approach you can start to grow your application and spread the responsabillity to your business model accros differente modules and view. It improves the quallity of your project and we start to see some [*single responsibility principle*](https://en.wikipedia.org/wiki/Single_responsibility_principle) pattern
 
