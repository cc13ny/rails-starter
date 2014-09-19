# 55minutes/rails-starter

**A simple template for starting new Rails 4 projects.**

## How this repository is organized

There are two branches of this project that are regularly maintained: `master` and `bootstrap`.

* The `master` branch contains the newest rails-starter template. Most projects are best served by starting from this branch.
* The `bootstrap` branch contains all the latest code from master, *plus* extra gems, views, and helpers specific to Twitter Bootstrap. If you are starting a project where you plan to use Twitter Bootstrap, the bootstrap branch is what you need.

## About rails-starter

Rails-stater is a project template for Rails 4 projects that is pre-configured for Capistrano-based deployment. This template targets the following server stack:

* Ubuntu 12.04 LTS
* PostgreSQL
* Unicorn
* Nginx
* rbenv
* [dotenv][]
* [Postmark][] for mail delivery

By using this template, you’ll hit the ground running with best practices for productive Rails and front-end development:

* RSpec and Capybara for testing
* guard-livereload for fast, iterative front-end development
* Up-to-date rbenv and bundler gem management techniques
* [SMACSS][] for organizing stylesheets
* Capistrano recipes to make deployment easy
* `.env` for storing encryption keys and secret tokens safely outside of source control
* An easy way to add Twitter Bootstrap, should you choose to do so (use the `bootstrap` branch)

More on our blog:

* [Lightning-Fast Sass Reloading in Rails 3.2][sass-reloading]
* [SMACSS and Rails – A Styleguide for the Asset Pipeline][smacss-rails]


## Prerequisites

This project requires:

* Ruby 2.1.3, preferably managed using [rbenv][]
* Qt (in order to build the [capybara-webkit][] gem)

For a complete Ruby development environment, please follow our blog post: [Rails OS X Developer Guide – Installing an rbenv-based Rails stack on Mavericks and Mountain Lion][osx-rails].


## Getting started

### Create a Rails project from the template

1. Download and extract either the [master][master-zip] (plain starter) or the [bootstrap][bootstrap-zip] (Twitter Bootstrap-themed starter) ZIP archive of the rails-starter repository; this will be the start of your new Rails project.
2. Globally replace `rails-starter` and `RailsStarter` with the desired name of your project.
3. `cd` into the project and run `git init && git add . && git commit -m "init"` to initialize a git repository.

### bin/setup

Run the `bin/setup` script. This script will:

* Check you have the required Ruby version
* Install gems using Bundler
* Create local copies of `.env` and `database.yml`
* Create, migrate, and seed the database

### Run it!

1. Run `rake spec` to make sure everything works.
2. Run `rails s` to start the app.


## Using the provided Capistrano 3.x recipes

This project uses the `capistrano-fiftyfive` gem, which provides all recipes needed to set up and deploy on Ubuntu 12.04. It's super simple.

### Purchase a VPS

Using a provider like [DigitalOcean](http://digitalocean.com), purchase an Ubuntu 12.04 LTS virtual private server. **Make sure to install your SSH key for the root user.**

Make note of the IP address of the VPS. Then:

### Change the deployment settings of your project

To use capistrano you will need to update the deployment settings to match your VPS.

1. Review the contents of `config/deploy.rb`. Be sure the change the `:repository` to match your git repository URL.
2. Update the IP address in `config/deploy/staging.rb` to match the IP of the VPS you just purchased.
3. By default, `cap production deploy` will deploy from the `master` branch, and `cap staging deploy` will deploy from the `development` branch. Update the branch settings if you use a different branch policy.

### Capistrano takes care of the rest!

Don't forget to `git push` your code so that capistrano can deploy it. Make sure you've pushed the branch that capistrano is expecting in `staging.rb`. Then run these commands and follow the prompts to install Nginx, SSL, PostgreSQL, Ruby (the whole stack!):

     cap staging provision
     cap staging deploy:migrate_and_restart


**Refer to the [capistrano-fiftyfive README][cap-55] more details and deployment instructions.**


[dotenv]:https://github.com/bkeepers/dotenv
[Postmark]:https://postmarkapp.com
[osx-rails]:http://blog.55minutes.com/2013/09/rails-os-x-install-guide/
[sass-reloading]:http://blog.55minutes.com/2013/01/lightning-fast-sass-reloading-in-rails-32/
[SMACSS]:http://smacss.com
[smacss-rails]:http://blog.55minutes.com/2013/01/smacss-and-rails/
[rbenv]:https://github.com/sstephenson/rbenv
[capybara-webkit]:https://github.com/thoughtbot/capybara-webkit
[master-zip]:https://github.com/55minutes/rails-starter/archive/master.zip
[bootstrap-zip]:https://github.com/55minutes/rails-starter/archive/bootstrap.zip
[r]:http://blog.55minutes.com/post/15353228566/invoke-rails-and-rake-faster-and-with-fewer-mistakes
[SimpleForm]:https://github.com/plataformatec/simple_form
[bootstrap-examples]:http://simple-form-bootstrap.plataformatec.com.br/articles/new
[Devise]:http://devise.plataformatec.com.br
[cap-55]:https://github.com/55minutes/capistrano-fiftyfive/#readme
