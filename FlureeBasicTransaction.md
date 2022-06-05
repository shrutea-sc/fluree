# Fluree Basic Transactions
## Update Data
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
## Upsert Data
you can upsert data in fluree if you have unique predicate marked
``` json
[
  {
    "_id": ["_predicate/name", "person/handle"],
    "upsert": true
  }
]
```
## Delete Data
### Delete a subject
``` json
[
  {
    "_id": ["person/handle", "zsmith"],
    "_action": "delete"
  }
]
```

### Delete a predicate
``` json
[
  {
    "_id": ["person/handle", "jdoe"],
    "age": null
  }
]
```
