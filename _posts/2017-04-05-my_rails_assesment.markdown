---
layout: post
title:  "My First Rails App"
date:   2017-04-04 20:59:29 -0400
---


Building my first rails app was awesome. It helped me put together everything I had learned throughout the course about rails. I especially  became comfortable using `form_for` helper and `fields_for` helper for the complex form I built.  I also learned how to use the devise gem which was fun.  Some of the lessons I learned:

If you want rails to generate a `field_with_errors` div for the nested part of the form you must add `accepts_nested_attributes_for :model` macro. It took me a while to figure this out because I was using a custom attribute writer to accept the nested attributes. After I added that macro, it created those error divs. Here is what my model looks like:

```
# appointment model

class Recipe < ApplicationRecord

has_many :ingredients

  accepts_nested_attributes_for :ingredients

 def ingredient_attributes=(attributes)
    self.ingredients = Ingredient.find_or_initialize_by(attributes)
 end
	
	
```

I also used the devise gem for my app. It was a challenge to customize it for my web app, but was worth it. I needed to add attributes to my user model and I learned how to customize devise to allow more attributes. All I needed to do was sanitize the attributes in order to update your user model. 

Here is how I did it: I added a `before_action` filter to my application controller called `:configure_permitted_parameters, if: :devise_controller?`. Then I added the `protected` method, and created a method `configure_permitted_parameters`. Here is what it looks like:

```
protected

  def configure_permitted_parameters
    added_attrs = [:attribute1, :attribute2, :attribute3, :attribute4]
    devise_parameter_sanitizer.permit :sign_up, keys: added_attrs
    devise_parameter_sanitizer.permit :account_update, keys: added_attrs
  end
```

Now my user model can accept other attributes. [Check out my repo to see it yourself](https://github.com/peacestone/chat-with-the-rabbi) 









