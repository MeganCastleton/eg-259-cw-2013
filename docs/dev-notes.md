# Development Notes

Some preliminaries. If you haven't already, set [my repo](https://github.com/cpjobling/eg-259-cw-2013.git) as your "upstream" so that you can
download these notes (and any updates to the code).

    git remote add upstream https://github.com/cpjobling/eg-259-cw-2013.git

Then fetch and merge the latest updates:

    git fetch upstream
    git merge upstream/master

## Setting up the libraries

As we will be using Backbone.js, it will be a good idea to have access to the [Backbone.js
documentation](http://backbonejs.org/) to hand.

It would also be good to download a developer version of Backbone.js and its dependencies [json2.js](https://github.com/douglascrockford/JSON-js) and [underscore.js](http://underscorejs.org/). I suggest that we store these in ``js/vendor`` in your forked copy of the project.

To set up the libraries we add the following to the ``index.html`` file (after the script that loads the ``bootstrap.js`` classes but before ``app.js`` is loaded).

````JavaScript
<script src="js/vendor/json2.js"></script>
<script src="js/vendor/underscore.js"></script>
<script src="js/vendor/backbone.js"></script>
````

## Simulating network storage

I suggest that we use the drop-in replacement for ``Backbone.sync()`` [backbone-localstorage.js](https://github.com/jeromegn/Backbone.localStorage). This will avoid the need to have a RESTful api at this stage of development. All the project and project selections data will be stored in the browser using [HTML5 Web Storage](http://docs.webplatform.org/wiki/tutorials/offline_storage). We can just load our dummy data into the appropriate collections when our App starts, and any changes we make will be persisted, locally, in the browser. Later, when we build a server, we can replace local storage by RESTful server storage by removing the library from the application.

To load ``backbone-localstorage.js``, download it ad add it to ``js/vendor``. Then include the following code after backbone.js itself has been loaded:

````JavaScript
<!-- This script replaces Backbone.sync() with a version that uses local strorage -->
<!-- Remove this when you have a proper restful back-end -->
<script src="js/vendor/backbone-localstorage.js"></script>
````

To set up local storage, set up the associated collection:

````JavaScript
MyCollection = Backbone.Collection.extend({
  model: MyModel,

  localStorage: new Backbone.LocalStorage('uique-id-for-store'),

  url: '#'
});
````

Now, any-time you access this `MyCollection` or one of its associated models, you will be accessing data from `localStorage` rather than the web.

## Thinking about the App

Now let's think about the following questions.

### Models

* What models will we need?
* What attributes will the models have?
* How can create some data to work with?

### Collections

* What collections will we need?

### Views

* What views will we need?

### Templates

* What templates will we need?

### Router

* What are our application routes?

### Events

* What events will we need?

## What shall we do first

The master slave view is the simplest place to start as it is a variation of the examples we have covered in Lectures.
You will need to define a ``Project`` model, and a ``ProjectList`` collection and arrange for these to be displayed on
screen as appropriate. You will need to define three views, a ``HomeView`` for the app as a whole, a ``ProjectView`` for displaying
the details of a single project and a ``ListView`` for displaying the project list. You will need an ``AppRouter`` and some event
handlers. 

I also recommend that you use templates to avoid coding long HTML strings inside yoour views' ``render`` methods. The HTML examples provided are already set up with the correct columns and styles, and can be
used as the basis for your view templates.

Any questions, please use the issue queue.

Good luck,

Chris Jobling
8 March 2013
