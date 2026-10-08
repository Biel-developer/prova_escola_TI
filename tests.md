# Casos de Teste e Borda - Boundary Tests

> a regra de negócio do teto diário limita a cobrança máxima em 8000 centavos, mesmo se eu tentar passar disso

### 1. Testes de Fração e Tolerância
Parâmetros da minha variante: tolerância = 10 min, fração = 15 min a 100 centavos cada, teto = 8000 centavos.

| Minutos | Frações | Valor Esperado | Explicação do Caso |
| :--- | :--- | :--- | :--- |
| 5 min | 0 | 0 | Está dentro dos 10 min grátis |
| 10 min | 0 | 0 | Limite exato da tolerância gratuita |
| 11 min | 1 | 100 | Passou 1 min da tolerância: perde o benefício e cobra a primeira fração cheia |
| 15 min | 1 | 100 | Borda exata da primeira fração de 15 min |
| 16 min | 2 | 200 | Entrou 1 min na segunda fração, já arredonda pra cima |
| 30 min | 2 | 200 | Borda exata da segunda fração |
| 1300 min | 87 | 8000 | Bruto daria 8700 centavos, mas bate no teto de 8000 |

### 2. Casos de Teste pro Arredondamento do UC4

| Minutos dos Bilhetes Encerrados | Média Calculada | tempo_medio_minutos | Regra |
| :--- | :--- | :--- | :--- |
| [47, 48] | 47.5 | 48 | Ponto flutuante .5 tem que subir pra cima |
| [44, 46] | 45.0 | 45 | Valor cravado exato |
| [40, 41, 41] | 40.66 | 41 | Arredondamento comum |
| [] | 0.0 | 0 | Nenhum carro fechado na data |

### 3. Matriz de Validação de Erros e Precedência

| Endpoint | Contexto / Estado | Entrada | Status | Mensagem |
| :--- | :--- | :--- | :--- | :--- |
| POST /bilhetes | Placa já aberta no sistema | `{"placa": "123"}` | 422 | `{"erro": "placa_invalida"}` - validação antes do conflito |
| POST /bilhetes | Placa já aberta no sistema | `{"placa": "ABC1D23"}` | 409 | `{"erro": "bilhete_em_aberto"}` |
| POST /bilhetes/1/cancelamento | Bilhete já foi encerrado | `{}` | 409 | `{"erro": "bilhete_nao_aberto"}` |
| POST /bilhetes/1/encerramento | Bilhete já foi encerrado | `{}` | 409 | `{"erro": "bilhete_ja_encerrado"}` |
| GET /relatorios/diario | N/A | `?data=2026/10/05` | 422 | `{"erro": "data_invalida"}` |