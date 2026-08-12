## 🔗 Tarefa Monday
```text
https://vexur-company.monday.com/boards/18369698855/pulses/12764882924
```

## Query - correção de endereco

```cypher
LOAD CSV  with headers FROM 'https://s3.amazonaws.com/qv-docs-v2.vexur.com.br/22cad51d-fa6f-4b9e-98a5-dbc6e15b2060.csv' AS row FIELDTERMINATOR '|'
return count(row)
```
