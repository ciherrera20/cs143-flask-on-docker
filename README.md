# Flask on Docker

## Overview

A simple web app with the ability to display static content, as well as save and display user uploaded images. There are two versions: a development and production version. The development version runs a python webserver using Flask as the framework and uses Postgres to manage the app's database. The production version adds on Gunicorn to run the server and nginx as a reverse proxy. Each of these services is run in its own docker container. See this [tutorial](https://testdriven.io/blog/dockerizing-flask-with-postgres-gunicorn-and-nginx) for the full details.

![](https://github.com/ciherrera20/cs143-flask-on-docker/blob/master/webapp.gif)

## Build Instructions

### Development version:

If the web app's development version is currently running, bring it down with
```
docker-compose down
```
Add the `-v` flag to remove uploaded user content and the database

Run the web app with
```
docker-compose up -d --build
```

### Production version:

If the web app's production version is currently running, bring it down with
```
docker-compose -f docker-compose.prod.yml down
```
Add the `-v` flag to remove uploaded user content and the database

Run the web app with
```
docker-compose -f docker-compose.prod.yml up -d --build
```
Create/reset the database with
```
docker-compose -f docker-compose.prod.yml exec web python manage.py create_db
```

###  Using the web app
Both the development and production versions of the web app are hosted on `localhost:1342`. Navigate to [http://localhost:1342](http://localhost:1342) to check whether it is running. If it is, the following text should be displayed:
> {"hello":"world"}

Any files placed in the project's `./services/web/project/static` directory can be displayed by navigating to [http://localhost:1342/static/\<filename\>](http://localhost:1342/static/hello.txt).

Users can upload images at [http://localhost:1342/upload](http://localhost:1342/upload) which can then be displayed at [http://localhost:1342/media/\<filename\>](http://localhost:1342/media/<filename>).
