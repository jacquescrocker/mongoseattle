!SLIDE smbullets

# Extras

* Dirty Attributes
* Versioning
* Timestamps
* Keys
* Indexes
* Caching

!SLIDE

# Dirty Attributes

!SLIDE

# Dirty Attributes

    @@@ ruby
    person = Person.where(:first_name => "Jake").first

    # anything changed?
    person.changed? # =>  false

    person.first_name = "Toruk"

    # now has anything changed?
    person.changed? # =>  true

    # first name change?
    person.first_name_changed? # => true

!SLIDE

# Dirty Attributes: Tracking changes

    @@@ ruby
    person.changed? # =>  true

    person.first_name_was # => "Jake"

    person.first_name_change #  => [ "Jake", "Toruk" ]

    person.changes # => { "first_name" => [ "Jake", "Toruk" ] }

!SLIDE

# Versioning

    @@@ ruby
    class Person
      include Mongoid::Document
      include Mongoid::Versioning
    end

    person.first_name # => "Jake"
    person.update_attributes(:first_name => "Toruk")

    person.first_name # => "Toruk"
    person.versions.last.first_name # => "Jake"

!SLIDE

# Timestamps

    @@@ ruby
    class Person
      include Mongoid::Document
      include Mongoid::Timestamps
    end

    person = Person.create(:first_name => "Jake")
    person.created_at # Fri Apr 30 19:09:31 UTC 2010
    person.updated_at # Fri Apr 30 19:09:31 UTC 2010

    person.update_attributes(:first_name => "Toruk")
    person.created_at # Fri Apr 30 19:09:31 UTC 2010
    person.updated_at # Fri Apr 30 19:09:33 UTC 2010


!SLIDE

# Indexes

    @@@ ruby
    class Person
      include Mongoid::Document

      index :last_name, :unique => true
    end

    # index creation can sometimes take a long time...

    # so we only create them when you want them:
    rake db:create_indexes
