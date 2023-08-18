---
tags: development
#development 
---
<iframe width="560" height="315" src="https://www.youtube.com/embed/videoseries?list=PLA7e3zmT6XQXIpzDpu17FD4GqejDsVO4D" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/H_U2Bu75Ohc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/videoseries?list=PLiwhu8iLxKwL1TU0RMM6z7TtkyW-3-5Wi" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>


---

### What is graphql?
graphql is an alternative to RESTFUL API

there are 3 major operations which can be performed in graphql

query: to fetch value
mutation: allows to change the data
subscription: it will allow to watch for change

---

According to the second video:

first we create a graphql schema

we create the schema in /resources/graphql directory

```graphql
type Employee{  
id: ID!  
name:String  
salary:String  
departmentId:ID!  
}
```

here the type identifier is used to declare employee object
(!) makes it a mandatory field which means it is not nullable

Mutations:
this type represents the entry point for performing write operations in graphql api

---

