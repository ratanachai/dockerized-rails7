# Do these in order to start your Rails 7 project

```bash
# Create your own .env file 
cp .env.example .env

# Change all <myapp> to your app_name, as well as <changeme> to your DB password
code .

# Generate new rails app with postgres
docker-compose run app rails new . --force --skip-bundle --database=postgresql

# Update Gemfile.lock
docker-compose run app bundle update

# Inside the container: Add below to database.yml in default section
default: &default
  host: db
  username: <app_name>
  password: <%= ENV['POSTGRES_PASSWORD'] %>

# Then create DB
docker-compose run app rails db:create

# Start the app and you should see Rails welcome screen on http://localhost:3000/
docker-compose up
```
