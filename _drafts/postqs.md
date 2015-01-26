I've written an API with Flask that takes some input parameters, does some calculations and returns JSON. Pretty standard. Today I wanted to change it so that some of the parameters could be provided as lists and the API would return results for all combinations. So original query string would look something like this:

    ?a=10&b=20&c=hello

which would return:

    {
      "a": 10,
      "b": 20,
      "c": "hello",
      "result": 30
    }

And I wanted to be able to do this:

    ?a=10,20&b=20,30&c=hello

which should return:

    {
      "data": [
        {
          "a": 10,
          "b": 20,
          "c": "hello",
          "result": 30
        },
        {
          "a": 10,
          "b": 30,
          "c": "hello",
          "result": 40,
        },
        {
          "a": 20,
          "b": 20,
          "c": "hello",
          "result": 40,
        },
        {
          "a": 20,
          "b": 30,
          "c": "hello",
          "result": 50,
        }
      ]
    }

First goal: accept the above query string

    - has to be able to accept single, none and multiple values
    - try different if statements
    - find `ast.literal_eval` which does a pretty good job but seems a bit hacky
    - also needed to cast to a list properly
    - test the new method with `requests`
    - find out that requests creates the query string differently when passed an array
    - find out that this is the correct way to create an array of an input
    - find out that the `request.args` object in Flask/Werkzeug has a `getlist` method
      which does the whole thing. returns empty list if nothing given, can cast to
      the correct type, seems to handle all the edge cases
    - was tempted to stop after implementing the `literal_eval` approach, because
      it worked, but much happier with this method, which is more compliant and
      has less code.
