## 🔗 Tarefa Monday
```text
https://vexur-company.monday.com/boards/18369698855/pulses/12785176436
```

## Query - correção de endereco

```cypher
LOAD CSV  with headers FROM 'https://s3.amazonaws.com/qv-docs-v2.vexur.com.br/c954f43c-aa36-45cd-9438-729221f7ddfb.csv' AS row FIELDTERMINATOR '|'
return count(row), row
```
