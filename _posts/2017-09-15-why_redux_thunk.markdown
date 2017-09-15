---
layout: post
title:  "Why Redux Thunk "
date:   2017-09-15 03:09:50 +0000
---

When I started learning how to use Redux, I was introduced to the Redux Thunk library. At that time I did not have a good grip on Redux, and learning another JS library was exactly what I did not need. After I wrote my first app using Redux, I felt the time was ripe to read up and write about why Redux Thunk is needed.

By default, `dispatch()` can only take actions in the form of objects. In other words action creators can only return objects. If an API call or procedure is needed to be  run before `dispatch()`,  we will need to pass around `dispatch()` as props. Then once we have a prop called `dispatch()`, we can create a function that will run whatever procedures that we want, and call `dispatch()` afterwards.

In small applications, that works fine. But once we get to bigger applications, passing `dispatch()` as props does not go down well with the [idea of separating presentational and container components](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0).

Redux Thunk is all about solving this issue. It allows our action creators to return functions.  When a function is dispatched, Redux Thunk middleware intercepts the function, and passes in  `dispatch()` as an argument to the action function. This allows for any procedure to be run prior to calling `dispatch()`. In my app, here is what my action creator looks like:

```
import fetch from 'isomorphic-fetch'

const fetchFlights = (flightInput) => {
  return (
    (dispatch) => {
     dispatch({type: 'LOADING_FLIGHTS'})
      fetch('http://localhost:3001/api/flights/find', {
      headers: {'Content-Type': 'application/json'},
       method: 'POST',
       body: JSON.stringify({flights: flightInput})
       //body: JSON.stringify(
         //{flights: {departure_city: 'ATL', arival_city: "JFK", departure_date: '2017-10-22'}})
        }
      )
       .then(response => {
         if (response.ok) {
         return response.json()
        }
        throw new Error(response.statusText)
       })

       .then((flights) => {
          dispatch({type: 'RECEIVE_FLIGHTS', payload: flights })})
     }
   )
 }

export default fetchFlights

```

The action creator returns a new function with `dispatch()` as an argument. It then fetches from the API,  parses the returned JSON, and finally dispatches. This all happens with out passing `dispatch()`  as props. 

Setting up React Thunk is simple. All that is needed is to import applyMiddleware and thunkMiddleware and add it to your store:

```
import { createStore, applyMiddleware, compose } from 'redux'
import thunkMiddleware from 'redux-thunk'

const store = createStore(Reducer, applyMiddleware(thunkMiddleware))

```

Happy coding!
