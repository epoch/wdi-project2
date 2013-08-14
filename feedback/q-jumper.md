
what you did well
------------------

* refreshing concept
* well done getting it up running on heroku
* covered a lot of ground in terms to technology and things learned
  - from frontend to backend
  - eg google maps api with popup, ajax. I can see you have a good grasp of the workflow
  - made used of foundation to add styling to buttons
* personal touch with the links on the footer


Where you could take the project further
-----------------------------------------

As a first time end user:

* When I first land on the site. It's a bit confusing
  - no quick way to find out how to use the site
  - many links has no effect when click:
    - eg kill a queue, cutting queues

* I understand you have to login for some of the links to work, but that's not obvious for end users, some suggestions:
  - add some clear directions for better user experience
  - do not show link that have no effect
  - add validation or feedback for new user form
  - add validation or feedback for create bid

* documentation - both technical and non technical
  - you can do better then one line for the readme file :)
  - instructions on how to bootstrap the application for development
  - status of the app, known bugs etc
  - consider an about section or help section or some clear directions on the home page

* needs lots more test
* positive side effect of refactoring logic from controllers to models is they will be easier to test

some notes about your code
---------------------------

* identation, especially in the map.js file
* the bids_controller contains too much logic that belongs to better places
  - consider moving some into methods in the bid model

in your bid.rb file

    validates_uniqueness_of :winner, :scope => :offer_id, :conditions => lambda { where(:winner => true) }

this is nice, though you can also consider adding an unique index in the bids table to ensure uniqueness on the database level
  
