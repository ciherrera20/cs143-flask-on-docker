# Flask on Docker

## Project description

A simple web app with the ability to display static content, as well as save and display user uploaded files. There are two versions: a development and production version. The development version runs a python webserver using Flask as the framework and uses Postgres to manage the app's database. The production version adds on Gunicorn to run the server and nginx as a reverse proxy. Each of these services is run in its own docker container. The following tutorial was used: https://testdriven.io/blog/dockerizing-flask-with-postgres-gunicorn-and-nginx.

## Instructions

Development version:

If the web app's development version is currently running, bring it down with
```
docker-compose down
```
Add the `-v` flag to remove uploaded user content and the database

Run the web app with
```
docker-compose up -d --build
```

Production version:

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
