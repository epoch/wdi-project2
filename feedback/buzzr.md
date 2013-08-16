
what you did well
-----------------

* consistent colour scheme and theme
  - very nice map
  - animated sprites for ajax call

* interesting content
* responsive header and menu

Where you could take the project further
----------------------------------------

* user experience and feedback on user interactions:
  - consider replacing alert boxes with less intrusive status messages 
* would be nice if you can find a solution to Instagram's hipcups
* consider adding validations on both frontend and the backend
* a first class responsive experience would be nice, expecially the map


some notes about your code
-----------------------------

* indentation
* in your javascripts, variables are declared all over the place.
  - within a function, consider using single-var pattern to declare variables at the top of a function's scope
* you're testing for numeric equality of a property using the == operator, but you should probably be using === instead

You guys probably know this already, in the following, instead of == use ===

    if (photo.data.length == 0) {
        alert('Sorry, this photo has been marked private by the owner, try another marker!')
        return;
    };


* lots of unused files and code. Consider removing them from your code base
* Consider removing the instagram gem if you're not using it and wrap the instagram API calls with a HTTParty class

add a instagram.rb class to your models folder

    class Instagram
      include HTTParty
      base_uri "https://api.instagram.com/v1"

      def search(lat="-31.9530044", long="115.8574693")
        options = { :lat => lat, :lng => long, :distance => "50", :client_id => "efea46f4c52542348ced4c529263cf33" }
        url = "/locations/search.json"
        self.class.get(url, :query => options)
      end
    end

then you can do the following in the locations_controller point method:


    def points
      loc = Location.create( :address => params[:locale] )

      Instagram.new.search(loc.latitude, loc.lng)

      # makes the json data available for ajax
      render :json => @result
    end

I also added a small value of distance as a parameter ( distance=50 ) to fix the instagram time out errors