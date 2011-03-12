# has_permalink

A gem for generating url-safe permalink-string from any other attribute in the same ActiveRecord model.

Make you urls look like '/users/olkarls' instead of '/users/1'.

## Installation

put this in your gemfile:

    gem "has_permalink"

And run in your terminal:

    bundle install

If your model doesn’t already have the permalink attribute you can run this generator command:

    rails g has_permalink [Model]

That will generate a migration which adds a permalink attribute [Model] and indexes it. Don’t forget to:

    rake db:migrate

## Example

    class Post < ActiveRecord::Base
      has_permalink
    end

The plugin assumes that the permalink attribute is generated from the title attribute but it can be changed by providing an argument like this:

    class Post < ActiveRecord::Base
      has_permalink :heading
    end

The permalink attribute is generated by the before_validation callback and is only transformed if it’s blank. If it's not blank and you want to regenerate it use:

    @post.generate_permalink!

Use this syntax your controller:

    def show
      @post = Post.find_by_permalink(params[:id])
    end

## Updates

### 2011-03-12, version 0.0.8
* Removed the Rails 3 dependency.
* Updated homepage

### 2011-02-01, version 0.0.7:
* Permalinks can't start or end with '-'.
* Added class method for use in rake task.

### 2011-01-31, version 0.0.6:
* Fixed a bug where the permalink could sometimes remove characters.

Copyright (c) 2009 - 2011 Ola Karlsson, released under the MIT license
