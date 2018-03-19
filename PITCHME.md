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
@title[Query response]
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
@title[Mutation]
## Changing data ...
```
mutation {
  addReaction(input:{subjectId:"MDU6SXNzdWUyMTg2NjA4OTQ=", content:THUMBS_UP}) {
    reaction {
      id
      content
    }
  }
}
```

---
@title[Mutation response]
## ... also yields a response
```
{
  "data": {
    "addReaction": {
      "reaction": {
        "id": "MDg6UmVhY3Rpb24yMTA0MDU5Mw==",
        "content": "THUMBS_UP"
      }
    }
  }
}
```

---
@title[Building an API]
## Building an API
Many languages and libraries : Node.js, Java, Python, Clojure, Go, ...

We'll focus on Node.js

---
@title[Entry Point]
## Using the express framework
```javascript
var app = express()

app.use('/graphql', graphqlHTTP({
  schema: schema,
  rootValue: root,
  graphiql: true,
}))
```

---
@title[Schema]
## GraphQL schema syntax
```javascript
var schema = buildSchema(`
    type Query {...}
    type Mutation {...}
    ...
`)
```

---
@title[Types]
## Types
* Scalar types : Int, Float, String, Boolean, ID. You can define a new scalar
* Lists
* Object types : user-defined

---
@title[User]
## User type
```
"A User of the app"
type User {
    id: ID
    username: String
    name: String
    surname: String
    fullname: String
    role: Role
},
```

@title[User Query]
## User Query
```
type Query {
    "A single user by it's id"
    user(id: ID!): User
}
```

---
@title[Resolvers]
## Root resolver (using Sequelize)
```javascript
var root = {
    user: (args) => UserDB.findById(args.id).then(user => new User(user))
}
```

---
@title[User class]
## User class (and it's internal resolvers)
```javascript
class User {
    constructor(data) {
        this.id = data.id
        this.username = data.username
        this.name = data.name
        this.surname = data.surname
        this.roleID = data.roleId
    }

    fullname() { return this.surname + this.name }

    role() { return ... }
}
```

---
@title[GraphQL Explorer]
## Try it out !
[GitHub Graphql Explorer](https://developer.github.com/v4/explorer/)
