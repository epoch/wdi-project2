
what you did well
-----------------

* made good use zurb foundation
  - tabs control
  - buttons and forms styling
  - some what responsive
* made good use of different technologies from frontend to backend
  - external apis, ajax, frontend javascript, foundation styled controls
* I like how you only need a name and password to sign up


Where you could take the project further
----------------------------------------

* first and foremost - still a number of outstanding bugs
* some suggestions for geocoding related features
  - auto detect current location

* a first class responsive experience would be nice, chances of using this on a portable device would be high

* user experience:
  - consider adding more feedback & validations with javascript on the frontend when user performed an action sucessfully or unsucessfully  

* would be nice to able to press enter to perform a search as well as clicking on the search button
* documentation & readme file on github
  - instructions on how to bootstrap the application for development
  - status of the app, known bugs etc
  - consider an about section or help section or some clear directions on the home page

some notes about your code
-----------------------------

* needs to handle nils gracefully

if no cuisine was set for a restaurant, the following code will raise an error

    restaurant.cuisine.name


* consider using active record methods when querying data the database

for example, instead of this:

    @platscuisine = @plats.map{ |x| x.restaurant.cuisine.name }.uniq

try this:

    @platscuisine = @plats.uniq.pluck(:name)

* in your user model, instead of gecoding everytime user has been updated, consider to only geocode again when the address has changed 