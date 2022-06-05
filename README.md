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
and navigate to http://localhost:8090/
### creation of a ledger
```bash
my/ledger
```
### Adding a collection
``` json
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

``` json
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
### Adding Data
``` json
[
  {
    "_id": "person$jdoe",
    "handle": "jdoe",
    "fullName": "Jane Doe",
    "age": 25,
    "favNums": [1223, 12, 98, 0, -2],
    "favArtists": ["artist$1", "artist$2", "artist$3"],
    "follows": "person$zsmith",
    "favMovies": ["movie$1", "movie$2", "movie$3"]
  },
  {
    "_id": "person$zsmith",
    "handle": "zsmith",
    "fullName": "Zach Smith",
    "age": 63,
    "favNums": [5, 645, 28, -1, 1223],
    "favArtists": ["artist$1"],
    "follows": "person$jdoe",
    "favMovies": ["movie$2", "movie$3"]
  },
  {
    "_id": "person$anguyen",
    "handle": "anguyen",
    "fullName": "Amy Nguyen",
    "age": 34,
    "favNums": [7, 98, 0, 2],
    "favArtists": ["artist$2", "artist$3"],
    "follows": "person$jdoe",
    "favMovies": ["movie$3"]
  },
  {
    "_id": "person$dsanchez",
    "handle": "dsanchez",
    "fullName": "Diana Sanchez",
    "age": 70,
    "favNums": [9, 1950],
    "favArtists": ["artist$2"],
    "follows": "person$anguyen",
    "favMovies": ["movie$1", "movie$2", "movie$3"]
  },
  {
    "_id": "chat",
    "message": "Hi! I'm chat from Jane.",
    "person": "person$jdoe",
    "instant": "#(- (now) 20000)",
    "comments": ["comment$zsmith", "comment$anguyen"]
  },
  {
    "_id": "chat",
    "message": "Hi! I'm a chat from Diana.",
    "person": "person$dsanchez",
    "instant": "#(- (now) 5000)",
    "comments": ["comment$zsmithagain", "comment$anguyenagain"]
  },
  {
    "_id": "chat",
    "message": "Hi! I'm a chat from Zach.",
    "person": "person$zsmith",
    "instant": "#(now)"
  },
  {
    "_id": "comment$zsmith",
    "message": "Zsmith is responding!",
    "person": "person$zsmith"
  },
  {
    "_id": "comment$anguyen",
    "message": "Hi Jane!",
    "person": "person$anguyen"
  },
  {
    "_id": "comment$zsmithagain",
    "message": "Welcome Diana!",
    "person": "person$zsmith"
  },
  {
    "_id": "comment$anguyenagain",
    "message": "Welcome Diana! This is Amy.",
    "person": "person$anguyen"
  },
  {
    "_id": "artist$1",
    "name": "Gustav Klimt"
  },
  {
    "_id": "artist$2",
    "name": "Augusta Savage"
  },
  {
    "_id": "artist$3",
    "name": "Jean-Michel Basquiat"
  },
  {
    "_id": "movie$1",
    "title": "The Shawshank Redemption"
  },
  {
    "_id": "movie$2",
    "title": "Hot Fuzz"
  },
  {
    "_id": "movie$3",
    "title": "Gran Torino"
  }
]
```
