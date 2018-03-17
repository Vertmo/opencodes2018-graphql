@title[Introduction]
## GraphQL is cool
#### An introduction to your new query language

---
@title[What is it ?]
## What is GraphQL ?
Querying language developped by Facebook since 2012 and published in 2015. Alternative to REST APIs.

---
@title[Difference ?]
## I know REST, what's the difference ?
* Like REST, GraphQL is structured
* In REST, you query different endpoints : `/users/<username>` to get ALL the information about ONE user, `/users/<username>/repos` to get ALL the repositories of ONE user 
* In GraphQL, you query a single endpoint, and you get precisely what you ask for

---
@title[Query]
## My first Query ...
```
query {
  user(login:"vertmo") {
    name
    isCampusExpert
  }
}
```

---
@title[Response]
## ... and its response
```
{
  "data": {
    "user": {
      "name": "Basile Pesin",
      "isCampusExpert": true
    }
  }
}
```

---
@title[GraphQL Explorer]
## Try it out !
[GitHub Graphql Explorer](https://developer.github.com/v4/explorer/)
