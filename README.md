# Pythonapp-Heroku
Python app (AI model) using uwsgi and nginx deployed on heroku


Heroku has a free service model for small projects.It is a Platform as a Service that sits on top of AWS to provide an experience that is specifically designed to help developers to deploy,manage and scale their apps written in Ruby, Node.js, Java, Python, Clojure, Scala, Go & PHP.

If you want your application running on Heroku , you will have to know some commands on Heroku CLI & Dashboard.

The Heroku Command Line Interface (CLI) makes it easy to create and manage your Heroku apps directly from the terminal.
----------------------------------------------------------------------------------------------------------------------

The Heroku Dashboard is the primary web interface for interacting with the Heroku platform. It provides UI support for tasks 

like:


 
    • Creating Apps
    
    • Renaming Apps
    
    • Deleting Apps

 Prerequisites:
--------------------------------

    •  Git Installed on system

    •  Sign up for a Heroku account

    •  Install heroku CLI using:

$ sudo snap install --classic heroku


Scenario:
----------------

We are deploying Flask A.I Application.NGINX is the web server and reverse proxy, that passes requests on to uWSGI. uWSGI is an application server, which can communicate with the web server for receiving requests and forwards them to Flask via the WSGI protocol.


Step # 01:
-------------------
 
- Clone the Project from Github.

Ref: https://github.com/Cryptic-Gemini/Pythonapp-Heroku.git


Step # 02:
---------------------

- Set http-socket to :$(PORT) in uWSGI Configuration File (app.ini):

[uwsgi]

wsgi-file = app.py

callable = app

http-socket = :$(PORT)

processes = 4

threads = 2

master = true

chmod-socket = 660

vacuum = true

die-on-term = true

If you are using a service like Webfaction or Heroku to host your application, you can use http-socket .

http-socket sets workers to natively speak the http protocol. 
It is used to proxy uWSGI behind a webserver speaking http with backend.

http-socket = :$(PORT)


 It is required to bind the uWSGI socket to the port requested by the Heroku system (exported via the environment variable PORT we can access with $(PORT)).


Step # 03:
------------------
 
 - Make a Procfile to start your uWSGI instance.

                  web: uwsgi app.ini




Step # 04:
--------------------

- After you install the CLI, run the heroku login command. You’ll be prompted to enter any key to go to your web browser to complete login. The CLI will then log you in automatically.

                   $ heroku login

Step # 05:
-------------------------

- Initialize a local Git repository and commit your application code to it.

Note: You should initialize the Git repository in the app’s root directory.Otherwise it will not run when deployed on Heroku.

$ cd python-heroku

$ git init

$ git add .

$ git commit -m “My first commit”

Step # 06:
------------------

- Create a Heroku app:

         $ heroku create app-name

You can give any name of your choice instead of app-name.
For example :

        $ heroku create face-recognition-app

When you deploy your application on Heroku,you will have to choose a unique name for your application. 


Step # 07:
---------------

- Add a remote to your local repository


        $ heroku git:remote -a face-recognition-app



Step # 08:
------------------------

- Use the git push command to deploy your app on Heroku


            $ git push heroku master 


You will find your app running as:
-------------------------------

        Face-recognition-app.herokuapp.com

----------------------------------------------------------------------------------------------------------------------------
Summary:
----------------------------------------------------------------------------------------------------------------------------

git init

git add .

 git commit -m "My first commit"

heroku login

heroku create pyyhonface-recognition

heroku git:remote -a pyyhonface-recognition

git push heroku master

  https://pyyhonface-recognition.herokuapp.com
