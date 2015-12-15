---
layout: post

title: Introducing NextDev!
subtitle: "A User Interface for the IoT"
cover_image: nextdev-back.jpg

excerpt: "This is an excerpt"

author:
  name: Guy Molinari
  #twitter: wckoehler
  bio: Software Engineer, Architect, Entrepreneur
  image: logo.jpg
---
Article Body 1

> “Effective companies tend to communicate more, their people are curious and they have opinions”

More article text

##Some awesome code

{% highlight ruby linenos %}
def show
  puts "Outputting a very lo-o-o-o-o-o-o-o-o-o-o-o-o-o-o-o-ong lo-o-o-o-o-o-o-o-o-o-o-o-o-o-o-o-ong line"
  @widget = Widget(params[:id])
  respond_to do |format|
    format.html # show.html.erb
    format.json { render json: @widget }
  end
end
{% endhighlight %}

Nam ornare mi sit amet turpis tempus gravida. Donec
venenatis id est ut egestas. Nulla auctor fringilla tortor, a consectetur mauris consectetur molestie. Sed
molestie elit vitae pulvinar imperdiet. Quisque mauris sem, bibendum eget ornare at, blandit sit amet quam.
Nulla faucibus sed nisl vitae fermentum.
 
{% highlight ruby linenos %}
class User < ActiveRecord::Base
  has_many :user_assignments, :dependent => :destroy
  has_many :hospitals, :through => :user_assignments
  # 160 users
 
  # Ugly, but 5x faster than op2 and op3
  # Takes 2ms
  scope :grid_fields, -> { joins('LEFT JOIN user_assignments ON user_id = users.id LEFT JOIN hospitals ON hospitals.id = hospital_id').
                           group('users.id').select([:id, :name, :email, :role, 'min(hospitals.name) as first_hospital_name']) }
 
  # Brings in all 10 user columns and 36 hospital columns. Takes a long time to process all that data.
  # select() doesn't help - it's ignored
  # Takes 75ms
  scope :grid_fields_op2, -> { eager_load(:hospitals) }
 
  # 3 separate queries, User, UserAssignment, and Hospital.
  # User load - takes 1ms
  # UserAssignment - load takes 2ms
  # Hospital load - takes 7ms (selects all 36 columns - not easy to change this)
  scope :grid_fields_op3, -> { preload(:hospitals).select([:id, :name, :email, :role]) }
 
  # (needed for op2 and op3)
  # Note that when we use this function, the grid render is ~3x slower than just grabbing the raw
  # 'first_hospital_name' field from the first query. 100ms vs 30ms grabbing the raw field
  # def first_hospital_name
  #   hospitals.first.try(:name)
  # end
end
{% endhighlight %}

##Zoomable images

Image of the frong of NextDev

<div class="full zoomable"><img src="{{ site.baseurl }}/images/nextdev-front.jpg"></div>

That's all for now. Thanks for reading.
