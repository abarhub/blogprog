+++
title = "Exemple de requete en elasticsearch"
date = "2022-08-10"
description = "Exemple de requete en elasticsearch"
tags = ["elasticsearch","cheatsheet"]
summary = "Exemple de requete en elasticsearch"
+++
# Elasticsearch

Exemple de requete en ElasticSearch :
```http
POST my-index-000001/_search
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

Des sites avec d'autres exemples:
* https://gist.github.com/ruanbekker/e8a09604b14f37e8d2f743a87b930f93
* https://www.bmc.com/blogs/elasticsearch-commands/
* https://lzone.de/cheat-sheet/ElasticSearch
* https://elasticsearch-cheatsheet.jolicode.com/
