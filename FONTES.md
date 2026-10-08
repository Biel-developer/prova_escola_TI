# FONTES.md — Declaração de Consultas

> [!IMPORTANT]
> **Consulta é permitida — conteúdo sem rastreabilidade, não.**
> Preencha este arquivo **antes do push final** se você usou qualquer fonte
> além do seu próprio conhecimento e do material deste repositório. Se não
> usou nada, declare isso nas seções abaixo (transparência também conta ponto
> de confiança na correção).[^transparencia]

## 1. Sites / documentação consultados

> [!NOTE]
> **Só contam linhas numeradas da tabela** (`| 1 | <URL> | ...`). Links em
> texto corrido — inclusive o exemplo logo abaixo — **não são contados**
> como fonte declarada.

| # | URL | O que foi consultado | Onde aparece no entregável |
| --- | | --- | --- |
| — | | | |
| 1 | https://fastapi.tiangolo.com/tutorial/query-params-str-validations/ | Validação de query parameters e tipagem de strings | `plan.md` e `tasks.md` |
| 2 | https://docs.python.org/3/library/math.html | Funções matemáticas `math.ceil` e `math.floor` para arredondamento de frações | `spec.md` (UC2, UC4) e `plan.md` |
| 3 | https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Status | Semântica e precedência de códigos de status HTTP (404, 409, 422) | `constitution.md` e `tests.md` |
| 4 | https://docs.python.org/3/library/datetime.html | Manipulação de ISO-8601 e timezone offset (-03:00) | `constitution.md` e `spec.md` (UC1, UC4) |

*(Ex.: `https://docs.oracle.com/...` → sintaxe de `Optional` → `plan.md` na
seção de decisões. Esse link é ILUSTRATIVO — fora de linha numerada não
conta. Se nenhum site foi consultado, escreva: **"Nenhum site consultado."**)*

## 2. Uso de IA — **somente como consulta**


> [!WARNING]
> Usar IA **como agente** (ela edita arquivos, executa comandos, roda testes no
> seu lugar) é **proibido** e zera a prova. Usar IA como consulta (perguntas,
> explicações de conceito, revisão pontual, trechos que você copiou e entende) é
> permitido **desde que**:

1. a conversa seja **compartilhada** (botão Share) e o link fique **público**
   (ou acessível ao professor);
2. o link seja registrado abaixo, indicando **onde** o conteúdo foi usado;
3. você seja capaz de **explicar qualquer trecho** que a IA produziu — na
   dúvida, o professor pede o link e pergunta sobre o código.[^plagio]

| # | Link público da conversa | Onde o conteúdo foi usado |
| --- | --- | --- |
| 1 | https://gemini.google.com/app/b6ea85ae47877c36 | sobre precedência de status codes HTTP 422 vs 409 e modelagem de matriz de testes para frações e tolerância e Consulta técnica para validação de regras de negócio, estruturação de casos de borda | foi usado no spec.md , tests.md e constitution.md

*(Se nenhuma IA foi utilizada, escreva: **"Nenhuma IA utilizada."**)*

## 3. Compromisso

Declaro que todo o conteúdo deste repositório que não é de minha autoria direta
está declarado acima, e que consigo explicar qualquer trecho entregue — tenha
ele vindo da minha cabeça, de um site ou de uma IA consultada.

**Nome: Gabriel do Nascimento Cano Andrade / RA: 230005552**

[^transparencia]: Este arquivo é, ele mesmo, um exemplo de markdown bem
    usado: *alert* para a regra crítica, tabelas para os registros e *footnote*
    para justificativas. O mesmo padrão vale para os `.md` que você entregar.
[^plagio]: Rubrica comum da disciplina: conteúdo de LLM não declarado
    configura plágio e zera a prova — o link público da conversa é o que
    transforma "copiou" em "consultou".
