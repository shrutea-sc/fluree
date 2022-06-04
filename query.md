# Fluree Basic Query
## Update
``` json
[
  {
    "_id": ["person/handle", "dsanchez"],
    "age": 71
  }
]
```
update using subject id
``` json
[
  {
    "_id": 351843720888324,
    "age": 71
  }
]
```
## Delete
### Delete a subject
``` json
[
  {
    "_id": ["person/handle", "zsmith"],
    "_action": "delete"
  }
]
```

### delete a predicate
``` json
[
  {
    "_id": ["person/handle", "jdoe"],
    "age": null
  }
]
```
