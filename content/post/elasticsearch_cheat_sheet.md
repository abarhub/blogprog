+++
title = "Exemple de requete en elasticsearch"
date = "2022-08-10"
description = "Exemple de requete en elasticsearch"
tags = ["elasticsearch","cheatsheet"]
summary = "Exemple de requete en elasticsearch"
+++
# Elasticsearch

## Explications

Il y a 2 types de recherche :

| Type de recherche        | Score          | Cache |
| ------------- |:-------------:| -----:|
| Query      | Variable | Non |
| Filter      | Fixe      |   Oui |

Exemple :
```http
GET /_search
{
  "query": {
    "bool": {
      "must": {
        "match": {
          "message": "this is a test"
        }
      },
      "filter": [
        {
          "term": {
            "user": "kimchy"
          }
        },
        {
          "term": {
            "user": "herald"
          }
        }
      ],
      "must_not": {
        "term": {
          "user": "cassie"
        }
      },
      "should": {
        "term": {
          "user": "johnny"
        }
      }
    }
  },
  "aggs": {
    "user_terms": {
      "terms": {
        "field": "user"
      }
    }
  }
}
```

### Query String

Exemple :

```http
GET /_search
{
  "query": {
    "query_string": {
      "query": "(new york city) OR (big apple)",
      "default_field": "content"
    }
  }
}
```
les AND et les OR doivent être en majuscule


https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-query-string-query.html

### Simple Query



https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-simple-query-string-query.html

### Requetes


| Url        | Signification          |
| ------------- |:-------------:|
| GET _cat     | Information generale |
| GET /_cat/indices      | Liste tous les indexes      |
| GET /_cat/health      | L'etat du cluster Elasticsearch      |
| GET /      | La version d'elasticsearch      |
| GET _cat/aliases      | La liste des alias      |
| GET /<index>/_mapping      | Le mapping de l'index      |
| POST /<index>/_search      | recherche sur l'index      |
| POST /<index>/_search      | recherche sur l'index      |
| POST /<index>/_count      | comptage sur l'index      |


### les operateurs de recherche

https://coralogix.com/blog/42-elasticsearch-query-examples-hands-on-tutorial/


## Exemples

Exemple de requete en ElasticSearch :
```http
POST /my-index-000001/_search
{
  "query": {
    "match": {
      "[user.id](http://user.id/)": "kimchy"
    }
  },
  "fields": [
    "[user.id](http://user.id/)",
    "http.response.*",
    {
      "field": "@timestamp",
      "format": "epoch_millis"
    }
  ],
  "_source": false
}
```

Exemple trouvé [ici](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-fields.html)


```http
GET /_search
{
  "query": {
    "simple_query_string" : {
        "query": "\"fried eggs\" +(eggplant | potato) -frittata",
        "fields": ["title^5", "body"],
        "default_operator": "and"
    }
  }
}
```

```http
{
  "query": {
    "match": {
      "my_field": "meaning"
    }
  },
  "fields": [
    "name",
    "surname",
    "age"
  ],
  "from": 100,
  "size": 20
}
```

```shell
curl "localhost:9200/_search?q=name:john~1 AND (age:[30 TO 40} OR surname:K*) AND -city"
```


```shell
% curl 'localhost:9200/_cat/indices?format=json&pretty'
[
  {
    "pri.store.size": "650b",
    "health": "yellow",
    "status": "open",
    "index": "my-index-000001",
    "pri": "5",
    "rep": "1",
    "docs.count": "0",
    "docs.deleted": "0",
    "store.size": "650b"
  }
]
```

```shell
curl -X PUT 'http://localhost:9200/students' -d '{
   "mappings": {
     "student": { 
       "properties": { 
         "name":     { "type": "keyword"  },
         "degree"    { "type": "keyword" },
         "age":      { "type": "integer" }  
         },
       "properties": { 
         "performance": { "type": "keyword"  } 
         }
     }
   }
 }'
```


```http
GET /my-index-000001/_search
{
  "timeout": "2s",
  "query": {
    "match": {
      "user.id": "kimchy"
    }
  }
}
```

```http
GET /my-index-000001/_search
{
  "track_total_hits": true,
  "query": {
    "match" : {
      "user.id" : "elkbee"
    }
  }
}
```


Des sites avec d'autres exemples:
* https://gist.github.com/ruanbekker/e8a09604b14f37e8d2f743a87b930f93
* https://www.bmc.com/blogs/elasticsearch-commands/
* https://lzone.de/cheat-sheet/ElasticSearch
* https://elasticsearch-cheatsheet.jolicode.com/
