# Cucumber-Selenium-Headless-Browser-Testing
Headless Browser Testing With Capybara and Selenium

This guide covers continuous integration and heroku deploymnet with codeship and headless GUI & browser testing using tools like capybara and selenium webdriver etc.

Below are the steps you need to follow to run a basic test for your rails app.

1) Add below test group to your gemfile and run bundle install.
https://gist.github.com/abidvf/a333413a7cf12e02656f714287c8bde2

2) Run rails generate cucumber:install to generate some configuration and basic skeleton for getting on to write the test.

3) Setup your cucmber rails env.rb file inside support folder as in below gist link.
https://gist.github.com/abidvf/c0e1c9458025bfb4a164db5c5ea454a7

4) Install phantomjs and set its path in env.rb file.
https://www.npmjs.com/package/phantomjs

5) Add below code to your database.yml file.
test:
  adapter:  postgresql
  host:     localhost
  database: demo_test
  username: postgres
  password: password
  port: 5432

6) Create a folder with name po to create a page object class for handling all of your page objects there. e.g
https://gist.github.com/abidvf/f8207a87825e6cc0631640d2b2146969

7) Now create a file manage_login.feature inside features folder for writing your whole scenario in a descriptive language.This file serves as an automation test script. It can contain a single or even a multiple scenarios in a single file.
(You can change the scenarios as per your flow requirements)
For help:
https://github.com/cucumber/cucumber/wiki/Feature-Introduction
For example:
https://gist.github.com/abidvf/c6373fcbf2c57d65a5ea711658fd1a9b

8) Create file login_steps.rb inside step_definitions folder to run all of the steps that you have written inside feature file.
For example:
https://gist.github.com/abidvf/d99c97eb46b20b137a22c9d5be79281b

9) Once you have all done with above steps, run below command to execute your first test case.
bundle exec cucumber features/manage_pos.feature

## Codeship and heroku integration

10) Signup to codeship and create a project there and click to tests link.
11) Select ruby on rails as your technology.
12) Add below commands in setup commands section.

Markup : rvm use 2.2.0 --install
  bundle install
  export RAILS_ENV=test
  sed -i "s|5432|5434|" "config/database.yml"
  bundle exec rake db:create:all
  bundle exec rake db:migrate
  bundle exec rake db:seed
  
13) And in test command section add:
bundle exec cucumber features/manage_pos.feature
and then save changes.

14) Now click on deploy menu link to link your heroku repository.

When you push the code to heroku for deployment the login test case is first executed and after successfull execution it will be deployed to heroku server. :+1: :+1:




