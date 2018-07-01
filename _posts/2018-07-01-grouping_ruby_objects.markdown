---
layout: post
title:      "Grouping Ruby Objects"
date:       2018-07-01 13:38:20 -0400
permalink:  grouping_ruby_objects
---


Recently I started contributing to an open source project and learned along the way some new ruby methods that are used to group together a collection of ruby objects.

## group_by

Exactly as it sounds, `group_by` iterates over each item in the enumerable and return a hash with its keys set based on the return values from the block. For example:

```ruby

Event.all.group_by do |event|
      if event.starts_at < Date.today
        :past
      elsif event.starts_at.to_date == Date.today
        :today
      else
        :future
      end
    end
#=> {past: [event,...], today: [event], future: [event,...]}
```

The returned values from the running block will be past, today, and future hence our returned hash we will contain those three keys. The values of the keys will be set to whatever element the block's parameter evaluated to at the time the result was returned. In the example above, an event that started before today will be set as the value of the key past, and the event that is happening today will be set as the value for the key today etc.

## value_at

Say we have a hash with multiple keys and we would like to have returned back an array containing the values of each key in a specific order. The `values_at` method allows us to do just that. It gets called on a hash and takes as an argument all the keys you would like to be returned and returns back the values in the order they were inputted as arguments. For example:

```ruby
grouped_events =  {past: [event,...], today: [event], future: [event,...]}
events_array = grouped_events.values_at(today, future)
#=> [[event,...],[event,...]]
```

Now we can use multiple assignment to get each element:

```ruby

todays_event, future_events = events_array

```

Whats neat about reading someone else code is seeing how different it is was written from the way you would write it. I'm definitely going to be spending more time reading other people code and suggest anyone who wants to broaden their knowledge to do so.
