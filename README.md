## GraphQL Operation: Query

###### GitHub GraphQL Explorer

```GraphQL
{
  viewer{
    name
    url
  }
}
```

- The *viewer* is an **object** of in GraphQL term.
- Object hold data about an entity.
- The *Field* is is used for ask specific properties in objects, like object-name and object-url.


Once you run GraphQL
###### Github GraphQL Explorer

```GraphQL
{
  "data"{
    "viewer"{
      "name": "kristyyang"
      "url": "https://github.com/kristyhome"
    }
  }
}
```

You can pass **arguement** to Fields

```GraphQL
{
  organization(login: "to-road-to-learn-react"){
    name
    url
  }
}
```

result:

```GraphQL
{
  "data": {
    "organization":{
      "name": "The Road to learn React"
      "url": "https://github.com/the-road-to-learn-react"
    }
  }
}
```

##### If you have 2 Field as same arguement
- *Field* "organization" as an arguement conflict, then

```GraphQL
{
  book:organization(login: "to-road-to-learn-react"){
    name
    url
  }
}

{
  company:organization(login: "airbnb"){
    name
    url
  }
}
```

Resule in GraphQL Explorer
```GraphQL
{
  "data": {
    "book": {
      "name": "to-road-to-learn-react"
      "url": "https://github.com/to-road-to-learn-react"
    },
    "company": {
      "name" : "airbnb"
      "url" : "https://github.com/airbnb"
    }
  }
}
```

##### If you want to request same field in both organization,without duplication

We use **fragment** to extract the query reuse part

```GraphQL
{
  book: organization(login: "to-read-to-learn-react") {
    ...shareOrganizationFileds
  },
  company:organization(login: "airbnb"){
    ...shareOrganizationFileds
  }
}

fragment shareOrganizationFileds on Organization{
  name
  url
}
```

### GraphQL Operation: Mutation

- Shard same principle with mutation:
    - It has field and object, arguements and variables, fragment and operation names
    - Directives and nested object for returned result

```GraphQL
query {
  organization(login: "the-road-to-learn-react") {
    name
    url
    repository(name: "the-road-to-learn-react") {
      id
      name
      }
    }
}

```

####Before using the identifier as a variable, you can structure your mutation in GraphiQL the following

```GraphQL
mutation AddStar($repositoryId: ID!) {
  addStar(input: { starrableId: $repositoryId }) {
    starrable {
      id
      viewerHasStarred
      }
      }
}
```

And in Query variable

```GraphQL
{
"repositoryId": "MDEwOlJlcG9zaXRvcnk2MzM1MjkwNw=="
}
```

GitHub GraphQL Explorer

```GraphQL
{
"data": {
  "addStar": {
    "starrable": {
      "id": "MDEwOlJlcG9zaXRvcnk2MzM1MjkwNw==",
      "viewerHasStarred": true
      }
    }
  }
}
```

## GraphQL Pagination

It could take ages to fetch a list of repositories from a large organization.
In GraphQL, you can request paginated data by providing arguments to a list field.


**GitHub GraphQL Explorer**
```GraphQL
query OrganizationForLearningReact {
  organization(login: "the-road-to-learn-react") {
    name
    url
    repositories(first: 2) {
      edges {
        node {
          name
        }
      }
    }
  }
}

```
