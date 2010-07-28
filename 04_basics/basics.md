!SLIDE

# Ok... now for some code



!SLIDE

# Mongoid

    @@@ ruby
    class Person
      include Mongoid::Document

      field :first_name
      field :last_name
      field :arrival_date, :type => Date
      field :division
      field :clearance_level, :type => Integer, :default => 0

      embeds_many :assignments

      scope :security_personnel, where(:division => 'security')
    end

    jake = Person.security_personnel.where(:first_name => 'Jake',
                                           :last_name => 'Sully').first

!SLIDE

# Mongoid::Document

    @@@ ruby
    class Person
      include Mongoid::Document

      field :first_name
      field :last_name
      field :arrival_date, :type => Date
      field :division
      field :clearance_level, :type => Integer, :default => 0
    end

!SLIDE

# Embedded Associations

    @@@ ruby
    class Person
      include Mongoid::Document

      embeds_many :assignments
    end

    class Assignment
      include Mongoid::Document

      embedded_in :person
    end


!SLIDE

# "Relational" Associations

    @@@ ruby
    class Person
      include Mongoid::Document

      references_many :assignments
    end

    class Assignment
      include Mongoid::Document

      referenced_in :person
    end

!SLIDE

# Validations (ActiveModel)

    @@@ ruby
    class Assignment
      include Mongoid::Document

      field :name
      field :start_date, :type => Date
      field :end_date, :type => Date

      validates_presence_of :name, :start_date

      validates_uniqueness_of :name, :scope => :course_id

    end

!SLIDE

# Finders

    @@@ ruby
    Person.where(:first_name => "Grace")

    Person.where(:aliases => ["The Dude", ...])

    Person.where(:gender => "Male").and(:age.gt => 18)

    Person.excludes(:status => "Married")

    Person.in(:status => ["Single", "Divorced"])

    Person.where(:age.lte => 55)


!SLIDE smbullets incremental

# Lazy Evaluation

* All mongoid finders return a "Criteria" object

* Avoid execution of the query till the last possible moment

* mix/match queries, and extend queries already constructed

* Waits for a "kicker":

* `first`
* `entries`
* `each`
* `map`


!SLIDE

# Lazy Evaluation

    @@@ ruby
    grace = Person.where(:first_name => "Grace")

    puts grace
    #<Mongoid::Criteria:0x10362a3c8 @selector={:name=>"Grace"} ...>

    # extend the query dynamically
    grace_under_fire = grace.where(:status => "Fired")

    # give it a "kick"
    grace_under_fire.first #=> grabs the first entry
    grace_under_fire.entries #=> grabs all entries


!SLIDE

# Find or Create / Initialize

    @@@ ruby

    Person.find_or_create_by(:first_name => "Miles")

    person = Person.find_or_initialize_by(:first_name => "Miles")


!SLIDE

# Callbacks (ActiveModel)

    @@@ ruby
    class Person
      include Mongoid::Document

      field :first_name
      field :last_name

      before_save :update_current_location
    end

!SLIDE

# Persistence

    @@@ ruby
    grace = Person.new(:first_name => "Grace",
                       :last_name => "Augustine")
    grace.save

    jake = Person.create(:first_name => "Jake",
                         :last_name => "Sully")
    jake.update_attributes(:first_name => "Toruk",
                           :last_name => "Makto")

    miles = Person.create(:first_name => "Miles",
                          :last_name => "Quaritch")
    miles.destroy

    # Mongoid also supports rails3 nested forms

