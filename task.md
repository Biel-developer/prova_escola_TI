# Decomposição de Tarefas do Trabalho - Tasks

Passo a passo organizado para guiar a implementação da API:

- [ ] Tarefa 1: Estrutura inicial e infra para SDLC
  - Montar a pasta do projeto, criar o requirements.txt com FastAPI e Uvicorn.
  - Fazer o Containerfile expondo a porta 8001 e documentar a inicialização no README.md.

- [ ] Tarefa 2: Regras tarifárias e helpers
  - Implementar as funções de cálculo de valor: lógica da tolerância de 10 min, divisão de frações com teto a 100 centavos e limite pelo teto diário de 8000 centavos.
  - Criar função utilitária pra arredondar a média de tempo no padrão exigido, subindo em .5.

- [ ] Tarefa 3: Modelagem e rotas principais de bilhetes
  - Criar o banco SQLite com a tabela de bilhetes.
  - Implementar os endpoints de abrir bilhete no UC1, listar ativos no UC3 e a trava de não deixar placa duplicada abrir vaga no UC8.

- [ ] Tarefa 4: Fluxos de encerramento, cancelamento e histórico
  - Endpoint de encerramento aplicando o cálculo de tempo e cobrança no UC2.
  - Endpoint de cancelamento apenas para bilhetes abertos no UC5.
  - Endpoint de consulta de histórico por placa no UC6.

- [ ] Tarefa 5: Relatório diário e testes automatizados
  - Endpoint do relatório diário agregando apenas os carros encerrados no dia especificado no UC4.
  - Criar testes usando pytest pra cobrir os casos de borda mapeados no tests.md.