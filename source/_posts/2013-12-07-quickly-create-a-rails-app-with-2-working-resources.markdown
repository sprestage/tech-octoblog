---
layout: post
title: "Quickly create a rails app with 2 working resources"
date: 2013-12-07 14:48:17 -0800
comments: true
categories:
- rails
---

Intro
=======

I created this rails app in preparation to learn about resource associations.  This was the basic app I created before I implemented anything complicated.  It is a good demonstration of how to generate the rails app, the resources, and the tests.  I also go through several steps to get the app ready to be tested using minitest and also how to lock down the app from a security perspective.  

This is a simple rails app, with a pair of resources, Doctors and Patients.  


Preparation
=======

## Generate rails app
```
  $ rails _3.2.16_ new DoctorPatientTracker --skip-test-unit

  $ cd DoctorPatientTracker
```

## Prepare for testing
Edit Gemfile for some useful debugging gems.  Then run bundler
```
  $ bundle
```

## Secure your app
Tuck away RAILS_SECRET from /config/initializer/secret_token.rb to /config/application.yml and add /config/application.yml to .gitignore.

## Implement some basics
Add a home page, /app/views/home/index.html.erb
Add a home controller, /app/controllers/home_controller.rb
Add a default route to /config/routes.rb
  root :to => 'home#index'

---

# You should now have a working rails app


## Check in frequently
Check everything into git and git hub so yous have this default rails app set in stone.  

## Create 1st resource scaffold
Create the scaffold for the new resource, Doctor.
```
  $ rails g scaffold Doctor name:string --no-test-framework --no-assets --no-stylesheets --no-scss
```


## Migrate the DB for 1st resource
Migrate the database to pick up the changes.
```
  $ rake db:migrate
```

## Create tests for 1st resource
I know I should probably create all the tests first, but I feel so lost without the stuff there first, ya know.

Create the tests using generate, then completely replace what is in the files.
```
  $ rails g mini_test:feature DoctorShowIndex

  $ rails g mini_test:feature DoctorShow

  $ rails g mini_test:feature DoctorCreate

  $ rails g mini_test:feature DoctorUpdate

  $ rails g mini_test:feature DoctorDelete
```

Add /test/ folder.  Add /test/doctors/ folder.  Move doctor tests. Then
add fixture support to /test/test_helper.rb

## Modify views for 1st resource
Add Doctor name to display on /doctors/new page

Edit all the 5 /views/doctors/\*.html.erb to display the fields from the
models.

## Run the tests for 1st resource
Make sure all Doctor stuff works.
```
  $ rake
```

## Create 2nd resource scaffold
Time to implement Patients:
```
  $ rails g scaffold Patient name:string --no-test-framework --no-assets --no-stylesheets --no-scss
```

## Create tests for 2nd resource
Then create the Patient tests:
```
  $ rails g mini_test:feature PatientShowIndex

  $ rails g mini_test:feature PatientShow

  $ rails g mini_test:feature PatientCreate

  $ rails g mini_test:feature ItemUpdate

  $ rails g mini_test:feature ItemDelete
```

Add /test/patients/ folder.  Move patient tests.

## Migrate DB for 2nd resource
Add Patients to the DB:
```
  $ rake db:migrate
```

## Modify views for 2nd resource
Add Patient name to display on /patients/new page

Edit all the 5 /views/patients/\*.html.erb to display the fields from the
models.

## Run the tests for 2nd resource
Make sure all Patient stuff works.
```
  $ rake
```

# Final notes
You now have a working rails application with two resources, some minitests, a bit of security lockdown, and some useful views for the app.

Thank you for reading.  I hope you found this useful.
