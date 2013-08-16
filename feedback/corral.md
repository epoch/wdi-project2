
what you did well
-----------------

* well done getting it up and running on heroku
* nice clean, minialist interface, consistent design and a very nice styled map
* appreciate that I can browse before signing up
* overall quiet dummy proof, one of the most polished site out of all the project2s once up and running
* javascript code are nicely commented

Where you could take the project further
----------------------------------------

* consider adding posting comments via ajax as a progressive enhancement
* the side panel is starting to run out of room? 
* some subtle details like:
  - changing the cursor to a pointer when hovering on buttons on the top left and the buttons on the popup
  - clicking on the profile picture to show profile or edit profile as an option
  - do not show the remove image? checkbox when the user have yet to add an image to their profile 

* documentation
  - instructions on how to bootstrap the application for development
  - status of the app, known bugs etc
  - consider adding an about section or help section/popup as online documentation 

some notes about your code
-----------------------------

* seed.rb file has hard coded dependency

the leaf-green.png won't exist in my hard disk if I try to bootstrap the app in development:

    c1 = Category.create(:title => 'Relaxation', :image => File.open("/Users/jackjeffress/WDI/javascript/activityfinder/app/assets/images/leaf-green.png"))

* carrierwave is configured to use fog (amazon s3) in all environment (development & production)

in the image_uploader.rb file

    storage :fog 

consider making it dynamic based on the environment, so s3 is not required in development

in the layout.js file

  // The following compensates for the adding of the border from the Jquery UI library

  $('#panel').css({

   // Make the border unnoticable and hide the vertical scrollbar

   'width': '299px',
   'overflow-y': 'hidden'
  });

any reason why this css cannot be defined in a css file?

you probably know this already, best practice is to always declare variables with var

    var calculate_map_tiles = function() {
      n = 2 ^ zoom;
      x = ((latlong[0] + 180) / 360) * n;
      y = (1 - (ln(tan(latlong[1]) + sec(latlong[1])) / Pi)) / 2 * n;
    };

In the activities_controller.rb file:

    cats = []

    @categories.each do |category|
      cats.push({
                  :id => category.id,
                  :title => category.title,
                  :activities => category.activities,
                  :image => category.image.url
      })
    end

consider refactoring the categories json building process. 
 
In the following, the successfully deleted message will show even if @activity destroy failed:

If @activity has more than one user, the comparison to [current_user] will fail:

    def destroy
      @activity = Activity.find_by_slug(params[:id])
      #check user is the only user remaining and also the owner
      if @activity.users == [current_user] && owner?
        @activity.destroy
        redirect_to root_path
        flash[:notice] = "You successfully deleted the activity"
      else
        redirect_to root_path
        flash[:notice] = "You cannot delete an activity whilst it has other members"
      end
    end


consider refactoring this method into the activity model:

    def owner?
      @activity = Activity.find_by_slug(params[:id])
      current_user.memberships.where(:activity_id => @activity.id).first.role == 'owner'
    end