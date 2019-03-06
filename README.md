# Secondnature API

This is the database backend server structure for our app called Secondnature, a habit tracking app. This API was built with Ruby on Rails with Postgresql as the database system.

#### API Technical Details:

* Ruby version: 2.6.1

* Deployment site: Heroku

* Database creation (push into Postgreql):

```sql
CREATE TABLE habits (id SERIAL, habit_item VARCHAR(255), completed BOOLEAN, icon VARCHAR(255));
INSERT INTO habits (habit_item, completed, icon) VALUES (‘Practice Coding’, false, ‘/img/star.png’);
INSERT INTO habits (habit_item, completed, icon) VALUES (‘Meditate’, false, ‘/img/meditate.png’);
```
* Gem Deployment: 
```
bundle install
```

Routes Utilized:
```ruby
get '/habits', to: 'habits#index'
  get '/habits/:id', to: 'habits#show'
  post '/habits', to: 'habits#create'
  delete '/habits/:id', to: 'habits#delete'
  put '/habits/:id', to: 'habits#update'
```

#### Database initialization

Run ```postgres -D /usr/local/var/postgres```

#### Deployment instructions

If you haven't already, log in:

```heroku login```

Create your heroku app like normal:

```heroku create [my-app-name]```

You can now push just like you have in the past:

```git push heroku master```

Heroku is already set up to use Postgres, so you don't need any addons. To access your DB, log into heroku psql:

```heroku pg:psql```

Now you can copy the create/insert commands that you used for your local setup.

#### Issues with Heroku:

The biggest pain point we had with this project was the deployment of the API on Heroku. First, our initial repositories were not .git initialized for some reason so we had to recreate the repositories. Caroline was having issues with .zsh in her terminal, so she had to change the Ruby Version to 2.3.7 in order to get Heroku to recognize the folder. Richard was able clone the repository and changed the Ruby Version back to 2.6.1 and get the ```rails s``` command to work in terminal.

In habit.rb, we added the following code in order to connect Heroku to postgres:

```ruby
if(ENV['DATABASE_URL'])
    uri = URI.parse(ENV['DATABASE_URL'])
    DB = PG.connect(uri.hostname, uri.port, nil, nil, uri.path[1..-1], uri.user, uri.password)
else
    DB = PG.connect({:host => "localhost", :port => 5432, :dbname => 'habit_tracker_api_development'})
end
  ```
We made the mistake of adding the wrong ```DATABASE_URL```, thus creating issues with Postgres not being able to find the right database. This was not the only issue, so next we looked into the ```heroku logs``` in the terminal to determine the culprit(s).

One of the primary errors returned was:
```bash
2019-03-06T17:31:47.951962+00:00 heroku[router]: at=error code=H10 desc="App crashed" method=GET path="/" host=secondnature-api-5.herokuapp.com request_id=dbe5e2d7-313a-4b0a-8f42-4f3edd4dd35c fwd="47.41.35.143" dyno= connect= service= status=503 bytes= protocol=https
```
In order to get more detail, I then ran the heroku app within the console itself using the following command:
```
heroku run rails console
```
The rails app was able to run successfully on the console. Therefore, there was some type of issue with the state of the API between its launching via ```rails s``` and the Heroku app itself. Upon extensive searching on Google and StackOverflow, one solution suggested restarting heroku via the command ```heroku restart```.

Voila! This was the solution and we were able to launch our API via the Heroku deployment. In order to access the database you created earlier, you must enter the following link:

https://secondnature-api-5.herokuapp.com/habits

