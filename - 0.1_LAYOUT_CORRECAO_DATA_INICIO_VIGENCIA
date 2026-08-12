## 🔗 Tarefa Monday
```text
https://vexur-company.monday.com/boards/18369698855/pulses/12764846601
```

## Query - Ajustar a data vigência

```cypher
LOAD CSV  with headers FROM 'https://s3.amazonaws.com/qv-docs-v2.vexur.com.br/524ac329-82f0-493b-ac3d-de43936ae480.csv' AS row FIELDTERMINATOR ','

with * , datetime({
        year: toInteger(split(row["DATA_INICIO_VIGÊNCIA"], "/")[2]),
        month: toInteger(split(row["DATA_INICIO_VIGÊNCIA"], "/")[1]),
        day: toInteger(split(row["DATA_INICIO_VIGÊNCIA"], "/")[0]),
        timezone: "America/Sao_Paulo"
    }).epochMillis as dataInicioVigenciaFormatada

MATCH (ca:ContratoAdesao)
WHERE ca.numeroContrato  = toInteger(row["NUMERO_CONTRATO_VEXUR"])
MATCH (ca)--(bnf:Beneficiario)
MATCH (bnf)--(bc:BeneficioContrato)

// // // SET ca.inicioVigencia = dataInicioVigenciaFormatada
// // // SET bnf.dataInicio = dataInicioVigenciaFormatada
// // // SET bc.dataInicio = dataInicioVigenciaFormatada

RETURN ca.numeroContrato, row["NUMERO_CONTRATO_VEXUR"], apoc.date.format(ca.inicioVigencia) as dataVigenciaVexur, apoc.date.format(dataInicioVigenciaFormatada) as dataVigenciaMerlinNova
```
