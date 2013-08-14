
what you did well
-----------------

* still possibly the best reademe file in class
* very nice touch with the seeded statuses content :)
* good attempt at testing and TDD
* nice touch with showing human friendly timestamp/time ago
* nice touch with menu hover effect
* I like your ambition with the friends system

Where you could take the project further
----------------------------------------

* technical documentation
  - consider adding instructions on how to bootstrap the application for development in the readme file
  - status of the app, known bugs etc

* it seems twitter bootstrap didn't really help and was getting in the way
  - consider using a less intrusive library or try coding the css from scratch and just use media queries to make the site responsive

* still a lot of bugs that needs fixing

* I see you already have a list of todos in the readme, here is some other suggestions:
* a first class responsive experience would be nice. If I open up the site on a smaller screen device, the app should look like it was designed for the device
* user experience and feedback on user interactions:
  - consider adding more feedback (with javascript?) when user sucessfully or unsucessfully performed an action  
  - some links is not obvious where they lead to, for example:
    - I can only click on the time ago to get to a status? 
    - clicking of banter on the top left sometimes to feed sometimes to activities (intentional?)
    - menu hover effects are nice but they don't go anywhere

* consider a more coherent and consistent design (with stronger branding?) 
* you need to break down your test and think about what are you really testing, useful test is more important than coverage (let me know if you have questions)

some notes about your code
---------------------------

in the activities_controller.rb index method

    @activities = Activity.for_user(current_user, params)

why not do this instead? And you can further filter base on conditions as you see fit

    @activities = current_user.activities

instead of doing so many has_many in user.rb, consider adding filtering methods to the friendship class instead:

in user.rb

    has_many :friendships
    has_many :friends, :through => :friendships
    has_many :inverse_friendships, :class_name => "Friendship", :foreign_key => "friend_id"
    has_many :inverse_friends, :through => :inverse_friendships, :source => :user

in friendship.rb

    def self.pending
      where(:state => 'pending')
    end

    def self.blocked
      where(:state => 'blocked')
    end

so you can do this:

    current_user.friendships # will return all friendships in any state for the current_user
    current_user.friendships.pending # will return pending friendships for the current_user



