# Fluree

Fluree is an immutable graph database that, beyond performing typical modern database functions, emphasizes security, trust, provenance, privacy, and interoperability
## Install latest version of java 
it can also be created using docker and homebrew

```bash
sudo apt install openjdk-11-jre-headless 
```

## Install flurry

```bash
https://fluree-releases-public.s3.amazonaws.com/fluree-[MAJOR VERSION].[MINOR VERSION]-latest.zip
```

## export files and navigate to the folder to launch fluree

```bash
./fluree_start.sh
```
### creation of a ledger
```bash
my/ledger
```
### Adding a collection
``` sql
[
  {
    "_id": "_collection",
    "name": "person"
  },
  {
    "_id": "_collection",
    "name": "chat"
  },
  {
    "_id": "_collection",
    "name": "comment"
  },
  {
    "_id": "_collection",
    "name": "artist"
  },
  {
    "_id": "_collection",
    "name": "movie"
  }
]
```
### Adding Predicates

``` flureeql
[
  {
    "_id": "_predicate",
    "name": "person/handle",
    "doc": "The person's unique handle",
    "unique": true,
    "type": "string"
  },
  {
    "_id": "_predicate",
    "name": "person/fullName",
    "doc": "The person's full name.",
    "type": "string",
    "index": true
  },
  {
    "_id": "_predicate",
    "name": "person/age",
    "doc": "The person's age in years",
    "type": "int",
    "index": true
  },
  {
    "_id": "_predicate",
    "name": "person/follows",
    "doc": "Any persons this subject follows",
    "type": "ref",
    "restrictCollection": "person"
  },
  {
    "_id": "_predicate",
    "name": "person/favNums",
    "doc": "The person's favorite numbers",
    "type": "int",
    "multi": true
  },
  {
    "_id": "_predicate",
    "name": "person/favArtists",
    "doc": "The person's favorite artists",
    "type": "ref",
    "restrictCollection": "artist",
    "multi": true
  },
  {
    "_id": "_predicate",
    "name": "person/favMovies",
    "doc": "The person's favorite movies",
    "type": "ref",
    "restrictCollection": "movie",
    "multi": true
  },
  {
    "_id": "_predicate",
    "name": "person/user",
    "type": "ref",
    "restrictCollection": "_user"
  },
  {
    "_id": "_predicate",
    "name": "chat/message",
    "doc": "A chat message",
    "type": "string",
    "fullText": true
  },
  {
    "_id": "_predicate",
    "name": "chat/person",
    "doc": "A reference to the person that created the message",
    "type": "ref",
    "restrictCollection": "person"
  },
  {
    "_id": "_predicate",
    "name": "chat/instant",
    "doc": "The instant in time when this chat happened.",
    "type": "instant",
    "index": true
  },
  {
    "_id": "_predicate",
    "name": "chat/comments",
    "doc": "A reference to comments about this message",
    "type": "ref",
    "component": true,
    "multi": true,
    "restrictCollection": "comment"
  },
  {
    "_id": "_predicate",
    "name": "comment/message",
    "doc": "A comment message.",
    "type": "string",
    "fullText": true
  },
  {
    "_id": "_predicate",
    "name": "comment/person",
    "doc": "A reference to the person that made the comment",
    "type": "ref",
    "restrictCollection": "person"
  },
  {
    "_id": "_predicate",
    "name": "artist/name",
    "type": "string",
    "unique": true
  },
  {
    "_id": "_predicate",
    "name": "movie/title",
    "type": "string",
    "fullText": true,
    "unique": true
  }
]
```
