

# Convenção geral do projeto - Zona Azul Digital

Algumas regras que defini pro trabalho para manter o padrão da api e evitar bugs

- Dinheiro sempre em centavos (inteiros): mexer com `float` em finanças pode não ser muito bom por conta de aproximação binária, no caso não usar decimal e todo valor de grana vai ser número inteiro em centavos `valor_centavos`. Se a hora custa R$ 4,00, a gente trata como 400, podemos fazer da melhor forma
  
- Validação de entrada primeiro: tratar as requisições com fail-fast, se a requisição veio com schema quebrado ou placa errada, devolve erro 422, pois, não faz sentido bater no banco de dados se o dado de entrada nem é válido e o 422 sempre tem que vir antes do 409
  
- Fuso horário padrão: todas as datas que a API receber ou devolver precisam estar em ISO-8601 com o offset `-03:00` horário de Brasília
  
- Validação de Placa: a placa do carro tem que ter exatamente 7 caracteres alfanuméricos maiúsculos tipo `ABC1D23`, qualquer coisa com hífen ou letra minúscula toma 422
  
- Porta de execução: o servidor precisa rodar escutando na porta `8001`, que é a porta definida pela minha variante, sem precisar passar variável de ambiente extra