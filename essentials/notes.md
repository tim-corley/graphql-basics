### QUICKSTART

```
npm start
```

Note: if process already running, either change port (specified at index.js) or kill the process...

```
sudo lsof -i :8080
kill -9 50091 <pid>
```

_in new terminal window:_

```
mongod -dbpath=/Users/tcorley/Playground/Mongo/data/db
```

Navigate to: http://localhost:8080/graphql

### SAMPLE QUERIES & MUTATIONS

- Create new entry:

```
mutation {
  createFriend(input: {
    firstName: "Dennis"
    lastName: "Reynolds"
    gender: MALE
    age: 36
    email: "dennis@iasip"
    contacts: [
      { firstName: "Charlie", lastName: "Kelly" }
      { firstName: "Dee", lastName: "Reynolds" }
    ]
  }) {
    id
    firstName
    contacts {
      lastName
    }
  }
}
```

- Update Entry:

```
mutation {
  updateFriend(input: {
    id: "5ea1e5aa71d866806dd22dd2"
    firstName: "Charles"
    age: 39
  }) {
    firstName
    age
  }
}
```

- Delete Entry:

```
mutation {
  deleteFriend(id: "5ea1e83f9e6e6a6705cab939")
}
```

- Query Entry:

```
query {
  getFriend(id: "85ec02d3a5d4b7e9588a") {
    email
    contacts {
      firstName
      lastName
    }
  }
}
```

- Query All Entries:

```
{
	getAliens {
	  id
    firstName
    lastName
    planet
	}
}
```

- Using Aliases

```
query {
  one: getFriend(id: "5ea1e7859e6e6a6705cab937") {
    firstName
    lastName
  }
  two: getFriend(id: "5ea1e8229e6e6a6705cab938") {
    firstName
    lastName
    age
  }
  three: getFriend(id: "5ea1e5aa71d866806dd22dd2") {
    lastName
    email
  }
}
```

- Using Fragments

```
query {
  one: getFriend(id: "5ea1e7859e6e6a6705cab937") {
    ...friendFragment
  }
  two: getFriend(id: "5ea1e8229e6e6a6705cab938") {
    ...friendFragment
  }
  three: getFriend(id: "5ea1e5aa71d866806dd22dd2") {
    ...friendFragment
  }
}

fragment friendFragment on Friend {
  firstName
  lastName
  email
}
```

### TOOLS & REFERENCES

- https://wehavefaces.net/graphql-shorthand-notation-cheatsheet-17cd715861b6
- https://www.lynda.com/GraphQL-tutorials/GraphQL-overview/614315/702200-4.html
