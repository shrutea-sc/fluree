# Fluree Query
## Basic Query
### Select Key
The select-array can include any combination of the items in any order. A "*"
,Predicate Names: Namespaced or Not
,A map, crawling the graph.
,Reversely-referenced Predicates
or A map with sub-select options
### From key
A from key is used where your select options are applied to the field.
``` json
{
  "select": ["*", { "chat/_person": ["*", { "_as": "chperson" }] }],
  "from": [87960930223082, ["person/handle", "jdoe"]]
}
```
### Where Key
Where clauses are a simple way to apply very basic filters to a query
``` json
{
  "select": ["chat/message", "chat/instant"],
  "where": "chat/person = 351843720888322 OR chat/instant > 1517437000000"
}

```

## Analytical Query
Analytical query is used to answer more complicated questions about the data.
``` json
{
  "select": ["?nums", "(avg ?nums)"],
  "where": [["?person", "person/favNums", "?nums"]]
}
```
### Where key
#### Three Tuple
You define the values for one or two portions of a three-tuple when you include it in your where-array. Nulls or variables make up the sections you don't define.
#### Four Tuple
Four tuples are identical to three tuples with the exception that four tuples give a data source for the subject, predicate, and object patterns.
#### Two Tuple Variable Binding
Bind a variable to a value, including an aggregate value that has been computed. These variables can be utilised in the where-array items that follow.
``` json
{
  "select": "?person",
  "where": [
    ["?handle", "jdoe"],
    ["?person", "person/handle", "?handle"]
  ]
}
```
#### Binding map	
Serves the same function as a two-tuple variable binding, except the syntax is different.
#### Optional map	
Like, three-tuples, looks for flakes (pieces of data) that match a provided pattern. However, when joining the results of this map with the queries existing resultset, will simply bind null if there is no match (a left outer join).
#### Union map	
The two parts of a union map are outer joined.
#### Filter map	
Filters the results up to that point in the query.
``` json
{
  "select": ["?handle", "?num"],
  "where": [
    ["?person", "person/handle", "?handle"],
    ["?person", "person/favNums", "?num"],
    { "filter": ["(> 10 ?num)", "(= \"jdoe\" ?handle)"] }
  ]
}
```
### Prefixes key
If we wish to query across many Fluree ledgers, we may use the prefixes map to indicate the ledger.
```json
{
  "prefixes": {
    "ftest": "fluree/test"
  },
  "select": "?nums",
  "where": [
    ["$fdb4", ["person/handle", "zsmith"], "person/favNums", "?nums"],
    ["ftest", ["person/handle", "zsmith"], "person/favNums", "?nums"]
  ]
}
```
### Vars key
used to subsitute value in given query
```json
{
  "select": "?handle",
  "where": [["?person", "person/handle", "?handle"]],
  "vars": {
    "?handle": "dsanchez"
  }
}
```
## Block Query
this query is used to select all flakes from a block or a selection of blocks.
```json
{
  "block": [3],
  "prettyPrint": true
}

```
## Advanced Query
``` json
{
  "select": [
    "handle",
    { "comment/_person": ["*", { "_as": "comment", "_limit": 1 }] }
  ],
  "from": "person"
}
```
