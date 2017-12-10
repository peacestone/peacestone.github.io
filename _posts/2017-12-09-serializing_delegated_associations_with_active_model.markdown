---
layout: post
title:      "Serializing Delegated Associations with Active Model"
date:       2017-12-09 22:38:26 -0500
permalink:  serializing_delegated_associations_with_active_model
---


For my react app, I built a rails api for persisting flight reservations. I set up the database relations in a way that a reservation would belong to a flight, a flight would belong to a route, and a route would belong to an arrival and departure airport:


```
class Reservation < ApplicationRecord
  belongs_to :flight
end

class Flight < ApplicationRecord

  belongs_to :route
  has_many :reservations

end

class Route < ApplicationRecord
  belongs_to :arival_airport, class_name: 'Airport'
  belongs_to :departure_airport, class_name: 'Airport'

  has_many :flights

end

class Airport < ApplicationRecord

  has_many :arival_routes, class_name: 'Route', foreign_key: 'arival_airport_id'

  has_many :departure_routes, class_name: 'Route', foreign_key: 'departure_airport_id'

end


```



An issue I had  was how to associate reservations to a route  through a flight so a reservation can directly access all route attributes. 

After some research,  I read about the [delegate macro](https://simonecarletti.com/blog/2009/12/inside-ruby-on-rails-delegate/) that exposes a specific method that is defined on an associated object as your own method. In my case that would be the flight's route method becomes exposed as the reservation's own method through flights association with reservations. 


```
class Reservation < ApplicationRecord
  belongs_to :passenger
  belongs_to :flight
  after_create :generate_confirmation
  
delegate :route, to: :flight

end
```

For serialization I used active model serializers. At first I was not sure how I would serialize the delegated route object with its own associations (departure_airport and arrival_airport) to the reservation model. I thought that `belongs_to :route`  would not work in the reservation serializer model because route does not directly belong to a reservation and does not have a reservation id attribute. 

I decided to try it out anyways because what if `belongs to :route` in this context only invokes the delegated route association and serializes its return object. My guess turned out to be correct and the delgatated route object was serialized as well as its own belongs to associations (departure_airport and arrival_airport).

```
class ReservationSerializer < ActiveModel::Serializer

  belongs_to :passenger
  belongs_to :flight
  belongs_to :route

  attributes :id, :payment_info, :confirmation_number

end
```



I learned from this experience that when in doubt, trust your own instincts and don't give up.

[Checkout the projects github repo by clicking here](https://github.com/peacestone/juliet_airways_api)

