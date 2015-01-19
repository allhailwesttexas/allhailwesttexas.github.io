---
title: Accepting Arrays in the Query string with Flask
layout: post
---

I've written an API with Flask that takes some input parameters, does some
calculations and returns JSON. Pretty standard. Today I wanted to change it so
that some of the parameters could be provided as lists and the API would return
results for all combinations. So the original query string would look something
like this:

```javascript
?a=10&b=20&c=hello
```

which would return:

```javascript
{
    "a": 10,
    "b": 20,
    "c": "hello",
    "result": 30
}
```

And I wanted to be able to do this:

```javascript
?a=10,20&b=20,30&c=hello
```

which should return:

```javascript
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
```

- step1: arrays
- step2: ast.literal_eval - feels pretty hacky
- step3: notice what the `requests` module does
- step4: facilitate that
- result: clearer but more verbose