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
