# Fluree Query
## Basic Query
### Select Key
The select-array can include any combination of the following items in any order:
1.An *:
2.Predicate Names: Namespaced or Not
3.A map, crawling the graph.
4.Reversely-referenced Predicates
5.A map with sub-select options
### From key
A from key is used where your select options are applied to the field.
``` json
{
  "select": ["*", { "chat/_person": ["*", { "_as": "chperson" }] }],
  "from": [87960930223082, ["person/handle", "jdoe"]]
}
```
## Analytical Query
``` json

```
