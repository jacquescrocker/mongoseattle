!SLIDE bullets incremental

# Criteria

* Queries
* Sorting, Pagination, Limiting Data
* Geospatial Indexing
* Scopes

!SLIDE

# Find by id

    @@@ ruby
    Person.criteria.id("4bd9f19f2557ab0676000003").first

    # MongoDB query:
    find({:_id=>"4bd9f19f2557ab0676000003"}, {}).limit(-1)

!SLIDE

# Where

    @@@ ruby
    Person.where(:clearance_level.gt => 3).entries

    # MongoDB query:
    find({:clearance_level=>{"$gt"=>3}}, {})

!SLIDE

# `$all`

    @@@ ruby
    Person.all_in(:first_name => ['Grace', 'Jake']).entries

    # MongoDB query:
    find({:first_name=>{"$all"=>["Grace", "Jake"]}}, {})

!SLIDE

# `$in`

    @@@ ruby
    Person.any_in(:first_name => ['Grace', 'Jake']).entries

    # MongoDB query:
    find({:first_name=>{"$in"=>["Grace", "Jake"]}}, {})

!SLIDE

# `$ne`

    @@@ ruby
    Person.excludes(:first_name => 'Grace').entries

    # MongoDB query:
    find({:first_name=>{"$ne"=>"Grace"}}, {})

!SLIDE

# `$nin`

    @@@ ruby
    Person.not_in(:first_name => 'Jake').entries

    # MongoDB query:
    find({:first_name=>{"$nin"=>["Jake"]}}, {})

!SLIDE

# Sorting

    @@@ ruby
    Person.descending(:last_name).entries

    # MongoDB query:
    find({}, {}).sort([:last_name, :desc])

    Person.order_by(:name => :asc, :age => :desc).entries

    # MongoDB query:
    find({}, {}).sort([:name, :asc], [:age, :desc])


!SLIDE

# Pagination

    @@@ ruby

    # will_paginate compatible out of the box
    Person.paginate :page => params[:page], :per_page => 20

    # MongoDB query if params[:page] => 2
    find({}, {}).skip(40).limit(20)

!SLIDE

# Limiting returned fields

    @@@ ruby
    Person.only(:first_name, :last_name).entries

    # easy way to avoid the overhead of huge embedded fields

    # MongoDB query:
    find({}, {:_type=>1, :last_name=>1, :first_name=>1})

!SLIDE

# Geospatial Indexing

    @@@ ruby
    class Location
      include Mongoid::Document
      field :name
      field :lat_long, :type => Array
      index [[:lat_long, Mongo::GEO2D]]
    end

    Location.near(:lat_long => [30, 30])

    # MongoDB query:
    find({:lat_long=>{"$near"=>[30, 30]}}, {})

