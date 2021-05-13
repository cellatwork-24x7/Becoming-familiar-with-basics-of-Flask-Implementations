# Becoming-familiar-with-basics-of-Flask-Implementations
Flask is a popular Python web framework, meaning it is a third-party Python library used for developing web applications.Flask has three main dependencies. The routing, debugging, and Web Server Gateway Interface (WSGI) subsystems come from Werkzeug; the template support is provided by Jinja2; and the command-line integration comes from Click. These dependencies are all authored by Armin Ronacher, the author of Flask.  
Accessing databases, validating online forms, authenticating accounts, and other high-level activities are not supported natively in Flask. Extensions that connect with the main package include these and many other main features that most web apps need.  
As a developer, you have complete control over which plugins fit well for your project, and you can also write your own if you want to. In comparison, in a broader context, most decisions have already been taken for you and are difficult, if not impossible, to alter.

## Installation
To work with Flask web framework, a prior python installation is a must. To download Python, follow this link (https://www.python.org/downloads/), select the button that says Download Python 3.x.x, and then run the installer as you normally would to install applications on your operating system. The default settings should be fine.  To confirm that Python installed successfully, first open the command line. In macOS, click the spotlight icon on the top right corner of your desktop (the magnifying glass) and type terminal. The terminal should be the first application that appears. On Windows, click the Start menu icon and type cmd in the search box, then press Enter  Once your command line is open, enter these commands:  
      python --version  
      pip --version         
If the output for these commands includes a version number, Python is installed and available from the command line and you can proceed to the next step. Next, you’ll need to install Flask. At the command line, type  
      pip install flask  
This will install Flask using the pip package manager for Python. You should see some output ending in a notification that Flask has been installed successfully. As an alternative to the above installation instructions, you can install the Python 3 version of Anaconda, which can be downloaded here. Anaconda comes with Flask, so if you go this route you will not need to install Flask using the pip package manager.  

## Initialization
All Flask applications must create an application instance. The web server passes all requests it receives from clients to this object for handling, using a protocol called Web Server Gateway Interface (WSGI, pronounced “wiz-ghee”). The application instance is an object of class Flask, usually created as follows:  
      from flask import Flask  
      app = Flask(__name__)  
The association between a URL and the function that handles it is called a *route*. The most convenient way to define a route in a Flask application is through the app.route decorator exposed by the application instance. Functions like index() that handle application URLs are called view functions. If the application is deployed on a server associated with the www.example.com domain name, then navigating to http://www.example.com/ in your browser would trigger index() to run on the server. The return value of this view function is the response the client receives. If the client is a web browser, this response is the document that is displayed to the user in the browser window. A response returned by a view function can be a simple string with HTML content, but it can also take more complex forms.  

### A Complete Application
The hello.py application script defines an application instance and a single route and view function, If you have cloned the application’s Git repository on GitHub (https://github.com/cellatwork-24x7/flasky), you can now run git checkout 2a to check out this version of the application.
### Development Web Server
Flask applications include a development web server that can be started with the flask run command. This command looks for the name of the Python script that contains the application instance in the FLASK_APP environment variable. To start the hello.py application from the previous section, first make sure the virtual environment you created earlier is activated and has Flask installed in it.
### Debug Mode
Flask applications can optionally be executed in debug mode. In this mode, two very convenient modules of the development server called the reloader and the debugger are enabled by default.  
When the reloader is enabled, Flask watches all the source code files of your project and automatically restarts the server when any of the files are modified. Having a server running with the reloader enabled is extremely useful during development, because every time you modify and save a source file, the server automatically restarts and picks up the change.  
The debugger is a web-based tool that appears in your browser when your application raises an unhandled exception. The web browser window transforms into an interactive stack trace that allows you to inspect source code and evaluate expressions in any place in the call stack.  
**Note** : By default, debug mode is disabled. To enable it, set a *FLASK_DEBUG=1* environment variable before invoking flask run.
The flask command supports a number of options. To see what’s available, you can run flask --help or just flask without any arguments.
### The Request-Response Cycle
#### Application and Request Contexts
When Flask receives a request from a client, it needs to make a few objects available to the view function that will handle it. A good example is the request object, which encapsulates the HTTP request sent by the client. The obvious way in which Flask could give a view function access to the request object is by sending it as an argument, but that would require every single view function in the application to have an extra argument. Things get more complicated if you consider that the request object is not the only object that view functions might need to access to fulfill a request. To avoid cluttering view functions with lots of arguments that may not always be needed, Flask uses contexts to temporarily make certain objects globally accessible.

