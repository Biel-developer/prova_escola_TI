# Especificação de Requisitos e Casos de Uso spec

Especificação detalhada das regras de negócio que o agente precisa gerar:

### UC1 — Criar Bilhete (`POST /bilhetes`)

- Body esperado: `{"placa": "ABC1D23"}` e opcionalmente `"entrada": "<ISO-8601 com -03:00>"`
  
- Se a placa não tiver 7 caracteres alfanuméricos maiúsculos: retorna 422 `{"erro": "placa_invalida"}`
  
- Se o campo `entrada` vier preenchido mas fora do padrão ISO-8601: retorna 422 `{"erro": "entrada_invalida"}` e se não vier, assume o timestamp do momento
  
- Se o carro já tiver um bilhete aberto: retorna 409 `{"erro": "bilhete_em_aberto"}` conforme UC8
  
- Cenário feliz: Retorna 201 com `id`, `placa`, `entrada` e `status: "aberto"`

### UC2 — Encerrar Bilhete (`POST /bilhetes/{id}/encerramento`)

- Se o id não existir no banco: 404 `{"erro": "bilhete_nao_encontrado"}`
  
- Se o bilhete já tiver sido encerrado antes ou estiver cancelado: 409 `{"erro": "bilhete_ja_encerrado"}`
  
- Cálculo de tempo: calcula os minutos totais entre `entrada` e `saida`
  
- Regra da tolerância do UC7: se a duração for menor ou igual a 10 minutos, onde TOLERANCIA_MINUTOS = 10, o `valor_centavos` sai zerado como 0
  
- Regra de cobrança: se passou dos 10 minutos, como por exemplo 11 minutos, não tem desconto nenhum de tolerância, cobra tudo desde o minuto zero. O tempo é cobrado em frações de 15 minutos arredondando sempre pra cima via `ceil(minutos / 15)`
  
- Valor da fração: tarifa hora é 400 centavos, logo cada 15 min custa 100 centavos, divisão de 400 por 4
  
- Teto: se o total passar de 8000 centavos, limita no teto diário onde TETO_DIARIO_CENTAVOS = 8000
  
- Retorna 200 com: `id`, `placa`, `entrada`, `saida`, `minutos` e `valor_centavos` inteiro, nunca float

### UC3 — Listar Bilhetes Ativos (`GET /bilhetes/ativos`)

- Devolve 200 com array de bilhetes com status `"aberto"`
  
- Ordenar do mais novo pro mais antigo, ou seja, data de entrada decrescente. Se não tiver nada, devolve array vazio `[]`

### UC4 — Relatório Diário (`GET /relatorios/diario?data=AAAA-MM-DD`)

- Parâmetro `data` na query é obrigatório. Se não vier no formato `AAAA-MM-DD`, retorna 422 `{"erro": "data_invalida"}`
  
- Só entram na conta os bilhetes que foram encerrados naquele dia, conferindo a data de saída no fuso -03:00. Bilhetes que ainda estão abertos ou que foram cancelados ficam de fora
  
- Retorna 200 com: `data`, `total_bilhetes`, `faturamento_centavos` e `tempo_medio_minutos`.
  
- No cálculo da média dos minutos `tempo_medio_minutos`, quando der final .5, deve arredondar pra cima, como 47.5 virando 48. Se não tiver nenhum bilhete no dia, devolve zeros

### UC5 — Cancelar Bilhete (`POST /bilhetes/{id}/cancelamento`)

- Só pode cancelar se o bilhete estiver com status `"aberto"`. Se já tiver encerrado ou cancelado, devolve 409 `{"erro": "bilhete_nao_aberto"}`
  
- Se o ID não existir: 404 `{"erro": "bilhete_nao_encontrado"}`
  
- Se der certo: muda o status pra `"cancelado"`, não cobra nada e retorna 200, sem campos de saída e valor

### UC6 — Histórico por Placa (`GET /bilhetes?placa=ABC1D23`)

- Query `placa` obrigatória e se a placa for inválida: 422 `{"erro": "placa_invalida"}`
  
- Retorna 200 com a lista de todos os bilhetes daquele veículo, qualquer status, ordenados do mais recente pro mais antigo