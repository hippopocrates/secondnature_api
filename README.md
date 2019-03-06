# Secondnature API

This is the database backend server structure for our app called Secondnature, a habit tracking app. This API was built with Ruby on Rails with Postgresql as the database system.

API Details:

* Ruby version: 2.6.1

* Deployment site: Heroku

* Database creation (push into Postgreql):

CREATE TABLE habits (id SERIAL, habit_item VARCHAR(255), completed BOOLEAN, icon VARCHAR(255));
INSERT INTO habits (habit_item, completed, icon) VALUES (‘Practice Coding’, false, ‘/img/star.png’);
INSERT INTO habits (habit_item, completed, icon) VALUES (‘Meditate’, false, ‘/img/meditate.png’);

* Database initialization

Run ```postgres -D /usr/local/var/postgres```

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...
