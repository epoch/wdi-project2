
what you did well
-----------------

* very nice artwork and vector images
* good use twitter bootstrap to make the site mostly responsive
* polished branding and layout
* nice use of javascript carousel and tab views controls
* good effort with attempt to refactor views
* nice touch with showing human friendly timestamp/time ago
* made use and integrate with plugins, eg rails.validations.js 

Where you could take the project further
----------------------------------------

* a lot of links doesn't work ( I understand those features hasn't been implemented? )
* I can delete statuses belonging to someone else?
* client side validation with plugin is good, but more feedback on successful form submissions would be nice, both client server and server side messages
* consider doing integration/request test or controller test with views rendering enable to test the contents of the views because there are a lot of logic in your views
* or even better is to consider refactoring non presentation logic away from views 
* documentation & readme file on github
  - instructions on how to bootstrap the application for development
  - status of the app, known bugs etc

some notes about your code
-----------------------------

* code indentation in the templates can still improve
* for the end user there is still too many bugs  
* early test shows a few major app crashes due buggy code ( some were later fixed )
  - needs to handle nils gracefully

for example:

    status.user.username

if user is nil (ie the association between status and user is missing) calling username on it will fail

* carousel image breaks when window is resized
* favour using active record methods when querying data from the database, it's generally more performant

for example, instead of this:

    @chapters = Profile.all.map(&:chapter).uniq.sort

try this:

    @chapters = Profile.uniq.pluck(:chapter).sort
