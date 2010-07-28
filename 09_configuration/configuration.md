!SLIDE smbullets incremental

# Configuration

* Dynamic Fields
* Using ObjectIds
* Persisting type information
* Connections
* Configuring options
* Configuring logging

!SLIDE

# Dynamic Fields

    @@@ ruby
    class Location
      include Mongoid::Document

      field :lat_long, :type => Array
    end

    # save stuff that wasn't declared, you can then get access
    loc = Location.new(:name => "Tree of Voices")
    loc.name # => "Tree of Voices"


!SLIDE

# Intelligent Defaults

## `config/mongoid.yml`

    @@@ ruby

    development:
      # runs on localhost with default mongodb port
      database: myapp_dev




!SLIDE

# Works seamlessly on Heroku

## `config/mongoid.yml`

    @@@ ruby

    production:
      uri: <%= ENV[“MONGOHQ_URL”] %>

