---
layout: post
title:  "How To Handle No Returned Results From an API Query"
date:   2017-09-13 02:37:41 +0000
---


For my final assessment, I created a flight reservation application. The user enters a form that has a date, destination city, and arival citiy field. When the form is submited, an api call to the backend server is triggered to query for flights. If the server returns found flights, the user will see a componet with a list of flights. If the query returns no results, the user should only see a message component saying "the query returned no results". The first way I implemented the logic for this was to check the length of the returned flights list for the length of zero:

```
if (this.props.flights.flightsList.length === 0) {
   return <Message warning  size='huge' header='Sorry, no results were found!' />
  }
```

That worked, but it smelled like code. I wanted a cleaner interface, and that's when I had an idea. Before the server  returns to the client a list of flights, it should check to see if the collection of found flights is empty, and has no results:

```
      if flights.empty?
        render json: {error: "Their are no flights on the queried date"}
      else
        render json: flights, meta: {departure_city: requested_departure_city, arival_city: requested_arival_city,     departure_date:         Flight.format_date(requested_departure_day) }, meta_key: 'request'
      end
```

If there is no results, the server will return a JSON hash with an error key that has a value of an error message.
The client side checks for the error key in the returned flights lists hash, and if there is an error, will return an error message component:

```
if (this.props.flights.error) {
   return <Message warning  size='huge' header={this.props.flights.error} />
  }
```

Now my app is more readable and easy to work with!

You can check out my apps Github repo by [clicking here.](https://github.com/peacestone/juliet_airways)
