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

