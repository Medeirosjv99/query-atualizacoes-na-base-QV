## 🔗 Tarefa Monday
```text
https://vexur-company.monday.com/boards/18369698855/pulses/12764931335
```

## Query - Ajustar / reativar as ativas

```cypher
LOAD CSV  with headers FROM 'https://s3.amazonaws.com/qv-docs-v2.vexur.com.br/f7add4b8-1975-4161-8585-97b3105a9c08.csv' AS row FIELDTERMINATOR ';'

with * where row["STATUS"] = "ATIVO"

MATCH (ca:ContratoAdesao)--(bnf:Beneficiario)--(bc:BeneficioContrato)
where ca.numeroContrato = toInteger(row["NUMERO_CONTRATO_VEXUR"])
and ca.numeroMatriculaSistemaOrigem = row["CONTRATO_SISTEMA_ORIGEM"]
and bnf.nome = row["USUARIO"]

// // // set   bnf.dataFim = null,
// // //       bnf.formaCancelamento = null,
// // //       bnf.motivoCancelamento = null,
// // //       bc.dataFim = null

return distinct row["NUMERO_CONTRATO_VEXUR"], ca.numeroContrato, row["MOTIVO_CANCELAMENTO"] as solicitadoPelaQv, bnf.motivoCancelamento as naBaseVexur, bnf.dataFim as dataFimVexur, row["DATA_FIM_VIGENCIA"] as dataFimSolicitada, bnf.nome, row["USUARIO"]
```
---
## Query - Ajustar as canceladas obs: alguns ja estão ok verif.

```cypher
LOAD CSV  with headers FROM 'https://s3.amazonaws.com/qv-docs-v2.vexur.com.br/f7add4b8-1975-4161-8585-97b3105a9c08.csv' AS row FIELDTERMINATOR ';'

with * where row["STATUS"] = "CANCELADO"

MATCH (ca:ContratoAdesao)--(bnf:Beneficiario)--(bc:BeneficioContrato)
where ca.numeroContrato = toInteger(row["NUMERO_CONTRATO_VEXUR"])
and ca.numeroMatriculaSistemaOrigem = row["CONTRATO_SISTEMA_ORIGEM"]
and bnf.nome = row["USUARIO"]
// and bnf.dataFim is null

with * , datetime({
        year: toInteger(split(row["DATA_FIM_VIGENCIA"], "/")[2]),
        month: toInteger(split(row["DATA_FIM_VIGENCIA"], "/")[1]),
        day: toInteger(split(row["DATA_FIM_VIGENCIA"], "/")[0]),
        timezone: "America/Sao_Paulo"
    }).epochMillis as dataFimFormatada

// // // set   bnf.dataFim = dataFimFormatada,
// // //       bnf.formaCancelamento = 'Imediato',
// // //       bnf.motivoCancelamento = row["MOTIVO_CANCELAMENTO"]
// // //       bc.dataFim = dataFimFormatada

return distinct row["STATUS"], row["NUMERO_CONTRATO_VEXUR"], ca.numeroContrato, row["MOTIVO_CANCELAMENTO"] as solicitadoPelaQv, bnf.motivoCancelamento as motivoCancelamentoVexur, dataFimFormatada as dataFimSolicitada, bnf.dataFim as dataFimVexur, row["USUARIO"],  bnf.nome 
```
