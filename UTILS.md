# Utility Commands - ELK Stack + MyLoan

### Create messages index and message_content mapping

```json
PUT /prod_messages_v2
{
  "mappings": {
    "properties": {
      "message_content": {
        "type": "text",
        "fielddata": true
      }
    }
  }
}
```

### Reindex

```json
POST /_reindex
{
  "source": {
    "index": "prod_messages"
  },
  "dest": {
    "index": "prod_messages_v2"
  }
}
```

### Delete by query

#### Match all

```json
POST /prod_messages/_delete_by_query
{
  "query": {
    "match_all": {}
  }
}
```

#### Two terms

```json
POST /prod_messages/_delete_by_query
{
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "provider_id": 8
          }
        },
        {
          "term": {
            "loan_status": "pending"
          }
        }
      ]
    }
  }
}

```
