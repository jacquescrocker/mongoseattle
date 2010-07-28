!SLIDE bullets incremental

# Introducing Mongoid

* Built by Durran Jordan (@modetojoy)
* Object Document Mapper
* Easily define MongoDB backed Models
* Provides support for rich associations

!SLIDE bullets incremental

# Why Mongoid?
* Full Rails3 support
* Supports Atomic updates on records
* Chainable querying API
* Great documentation (mongoid.org)

!SLIDE bullets incremental

# Mongoid with Rails3

* Implements ActiveModel<br>(validations, form builders, etc)
* Seamless integration with Devise<br>(authentication framework)
* Works with rails3 generators<br>`rails generate model Post`

!SLIDE bullets

# Easy to Get Started

* `rails new my_app_name \ `
* `-m http://tiny.cc/mongoid-rails`


!SLIDE bullets incremental

# Atomic Updates on Records

* Problem with document oriented databases:
* What happens when 2 people are editing the same record?
* If we save the entire document, one person's changes can overwrite the other
* Even though they were editing different fields

!SLIDE bullets incremental

# Atomic Updates on Records (cont...)

* Mongoid keeps track of what changed
* And pushes only those updates to MongoDB when document changes
* `$set, $push, $pushAll, $unset`<br> http://www.mongodb.org/display/DOCS/Updating

!SLIDE bullets incremental

# BUT...


!SLIDE bullets incremental

# Don't be afraid of the Mongo Ruby Driver

* Mongoid gives you access at every step to the MongoDB Ruby Driver

* `Post.db #=> #<Mongo::DB:0x1037f6468 ...>`

* Ruby Driver tutorial: http://www.mongodb.org/display/DOCS/Ruby+Tutorial

* http://api.mongodb.org/ruby

!SLIDE bullets

# Mongoid helps get you started

* But it doesn't get in the way

* MongoDB has as great API

* When you need speed, skip the middleman. Use the driver


!SLIDE smbullets incremental

# But really... the reason Mongoid is so great...

* COMMMUNITY!

* Active IRC (#mongoid on freenode)

* Mailing List<br>http://groups.google.com/group/mongoid

* Tons of commit activity, from all over the globe

* It's about working together

* To build the best Ruby persistence framework ever