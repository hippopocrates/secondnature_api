# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version: 2.6.1

* System dependencies

* Configuration

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
