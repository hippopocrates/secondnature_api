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

* Issues with Heroku:

The biggest pain point we had with this project was the deployment of the API on Heroku. First, our initial repositories were not .git initialized for some reason so we had to recreate the repositories. Caroline was having issues with .zsh in her terminal, so she had to change the Ruby Version to 2.3.7 in order to get Heroku to recognize the folder. Richard was able clone the repository and changed the Ruby Version back to 2.6.1.

In habit.rb, we added the following code in order to connect Heroku to postgres:

```ruby
if(ENV['DATABASE_URL'])
      uri = URI.parse(ENV['DATABASE_URL'])
      DB = PG.connect(uri.hostname, uri.port, nil, nil, uri.path[1..-1], uri.user, uri.password)
  else
      DB = PG.connect({:host => "localhost", :port => 5432, :dbname => 'habit_tracker_api_development'})
  end
  ```
