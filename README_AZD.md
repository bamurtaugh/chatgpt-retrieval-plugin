open codespace
azd login --use-device-code
azd env new {your unique env name}
azd env set DATASTORE redis
azd env set BEARER_TOKEN footoken
azd env set OPENAI_API_KEY {your open ai key}
azd up

hit /docs endpoint to verify deployed

Run to get .env vars in current shell
```
source <(azd env get-values | awk '{print "export " $0}')
```

run curl command to insert data
```
curl -X POST ${SERVICE_API_URI}/upsert \
  -H "Authorization: Bearer footoken" \
  -H "Content-type: application/json" \
  -d '{"documents": [{"id": "doc1", "text": "Hello world", "metadata": {"source_id": "12345", "source": "file"}}, {"text": "How are you?", "metadata": {"source_id": "23456"}}]}'
```

// TODO
run query command to verify data inserted