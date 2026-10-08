# Decisões de Arquitetura e Planejamento - Plan

Anotações técnicas e justificativas de projeto para a geração da API:

1. Escolha da Stack - Python com FastAPI:
   - Optei por usar Python com FastAPI por ser um framework moderno, com validação automática de dados via Pydantic e muito rápido pra subir. Ajuda a manter a aplicação enxuta pro container.

2. Porta Fixa do Serviço - PORTA_SERVICO = 8001:
   - O servidor web Uvicorn vai rodar direto na porta 8001 pra bater certinho com o que a suíte de avaliação espera.

3. Banco de Dados Embutido - SQLite:
   - Como é uma API focada na lógica de negócio e não temos outros serviços rodando, usar SQLite em arquivo local ou em memória resolve perfeitamente sem precisar orquestrar container separado de PostgreSQL.

4. Tratamento Matemático dos Arredondamentos:
   - Como a função round padrão do Python usa arredondamento bancário jogando o final .5 pro par mais próximo, precisamos implementar explicitamente uma função que force o arredondamento pra cima via `math.floor(x + 0.5)`, respeitando o que foi pedido no UC4.
   - Todo cálculo de fração de tempo vai usar `math.ceil(minutos / 15)`.

5. Entregáveis de SDLC para o Critério D:
   - Criar um Containerfile enxuto rodando com usuário sem privilégios de root.
   - Criar requirements.txt com as dependências travadas e um README.md explicando como rodar o projeto localmente.