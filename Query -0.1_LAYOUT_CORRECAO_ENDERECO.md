## 🔗 Tarefa Monday
```text
https://vexur-company.monday.com/boards/18369698855/pulses/12764882924
```

## Query - correção de endereco

```cypher
LOAD CSV  with headers FROM 'https://s3.amazonaws.com/qv-docs-v2.vexur.com.br/d8fa070e-6eae-472f-b286-b574f8f273ae.csv' AS row FIELDTERMINATOR '|'
return count(row)
```
