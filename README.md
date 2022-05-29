# Putting it All Together: Client-Server Communication

## Learning Goals

- Understand how to communicate between client and server using fetch, and how
  the server will process the request based on the URL, HTTP verb, and request
  body
- Debug common problems that occur as part of the request-response cycle

## Introduction

Just like the last lesson, we've got code for a React frontend and Rails API
backend set up. This time though, it's up to you to use your debugging skills to
find and fix the errors!

To get the backend set up, run:

```console
$ bundle install
$ rails db:migrate db:seed
$ rails s
```

Then, in a new terminal, run the frontend:

```console
$ npm install --prefix client
$ npm start --prefix client
```

Confirm both applications are up and running by visiting
[`localhost:4000`](http://localhost:4000) and viewing the list of toys in your
React application.

## Deliverables

In this application, we have the following features:

- Display a list of all the toys
- Add a new toy when the toy form is submitted
- Update the number of likes for a toy
- Donate a toy to Goodwill (and delete it from our database)

The code is in place for all these features on our frontend, but there are some
problems with our API! We're able to display all the toys, but the other three
features are broken.

Use your debugging tools to find and fix these issues.

There are no tests for this lesson, so you'll need to do your debugging in the
browser and using the Rails server logs and `byebug`.

**Note**: You shouldn't need to modify any of the React code to get the
application working. You should only need to change the code for the Rails API.

As you work on debugging these issues, use the space in this README file to take
notes about your debugging process. Being a strong debugger is all about
developing a process, and it's helpful to document your steps as part of
developing your own process.

## Your Notes Here

- Add a new toy when the toy form is submitted

  - How I debugged:  I tried to submit.  It gave a 500 Internal Server Error and the Rails log "NameError (uninitialized constant ToysController::Toys):
  app/controllers/toys_controller.rb:10:in `create'". So I looked in the create controller.  The error said "Name error" so immediately I noticed the error in the Toy.create; it said Toys.create. 

- Update the number of likes for a toy

  - How I debugged:  I clicked the Like button, and it errored to the fetch request in client folder.  2 things, I knew the React was right, but I inspected it anyway.  The error said "Unexpected end of json", so I looked in the React code to inspect the json flow; it looked correct.  Then I went to the controller to inspect the json flow, and it was missing the render code.  I fixed the render code and it worked.

- Donate a toy to Goodwill (and delete it from our database)

  - How I debugged:  I clicked on the Slinky Dog Donate button and received a 404 error and the rails log: "Started DELETE "/toys/4" for 127.0.0.1 at 2022-05-29 09:41:55 -0500 ActionController::RoutingError (No route matches [DELETE] "/toys/4"):". So I looked in the routes file and noticed the :destroy method was missing.  I added it and successfully deleted Slinky Dog.
