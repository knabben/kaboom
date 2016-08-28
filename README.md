# kaboom

Code based on [rakyll/boom]  but instead of passing a single URL it is going to fetch a list of requests from Elasticsearch.

The idea is to replicate original traffic with control and good reporting. 

How to map it
---

Till now Amazon just have elasticsearch 1.5 available so I am using a deprecated library to fetch data from it.

You should ensure the followin mapping

```
  "uri": {
    "type": "string",
    "norms": {
      "enabled": false
    },
    "fielddata": {
      "format": "disabled"
    },
    "fields": {
      "raw": {
        "type": "string",
        "index": "not_analyzed",
        "doc_values": true,
        "ignore_above": 256
      }
    }
  },
  "req": {
    "type": "string",
    "norms": {
      "enabled": false
    },
    "fielddata": {
      "format": "disabled"
    },
    "fields": {
      "raw": {
        "type": "string",
        "index": "not_analyzed",
        "doc_values": true,
        "ignore_above": 256
      }
    }
  },
  "method": {
    "type": "string",
    "norms": {
      "enabled": false
    },
    "fielddata": {
      "format": "disabled"
    },
    "fields": {
      "raw": {
        "type": "string",
        "index": "not_analyzed",
        "doc_values": true,
        "ignore_above": 256
      }
    }
  }
```
Data can be parsed by an ELK stack, normally the requests are provided by NGINX log with filebeat, 
and parsed by Logstash to extract these fields.
