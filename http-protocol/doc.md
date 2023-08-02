# PROTOCOLO HTTP

Trabalha com o modelo de pedido > request e response.

Ele é o maestro que rege a internet.

Essa comunicação entre cliente e servidor é realizada com formato de texto com padrão bem definido.

## REQUEST

Tudo inicia na requisição, que é formada por:

1. Linha de pedido.
É formada por mais três informações:

> Identificador do método (método de requisição): basicamente o tipo de ação que se espera do servidor (GET, POST, etc).

> URI do Recurso: é o endereço no qual será enviado o pedido (/index.php).

> Versão do protocolo: http 1.1 que é versão mais adotada.

2. *Cabeçalho (header)*:
Nele passamos informações adicionais sobre a requisição, e o servidor pode responde de modo diferente dependendo dos campos e valores contidos nele. Existem dezenas de campos que podem ser enviados no cabeçalho de uma requisição. 

> DATE, AUTHORIZATION, CACHE-CONTROL, TRANSFER-ENCODING, ACCEPT, USER-AGENT, COOKIE, ETC. Ver mais em https://developer.mozilla.org/en-US/docs/Web/HTTP/Status?retiredLocale=pt-PT.

* Exemplo:
```
fetch("https://httpbin.org/get", {
  headers: {
    Date: new Date().toUTCString(),
  },
});
```

3. *Corpo ou mensagem (body)*: são os dados da requisição. 
É geralmente usado em requisições HTTP POST, PUT e PATCH, onde você deseja enviar informações adicionais, como dados de formulário, JSON, XML ou qualquer outro tipo de carga útil (payload).

Esse corpo pode enviar um objeto Json. 

> É importante lembrar que o tipo de conteúdo e a estrutura do corpo da requisição devem estar de acordo com o que o servidor espera para processar a requisição corretamente. Sempre consulte a documentação da API ou serviço para entender como o corpo da requisição deve ser formatado.

* *Exemplo contendo Linha de pedido, Header e body da Request*:

```
POST /api/create-user HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "username": "johndoe",
  "email": "john@example.com",
  "age": 30
}
```

## RESPONSE
O formato da resposta que o servidor pode nos retornar é composto também por 3 entidades:

1. *Linhas de Status*: é a primeira linha da resposta e contém três elementos: a versão do protocolo HTTP, o código de status e uma breve descrição textual do código de status.

> Versão do protocolo: 	httpp/1.1 para comunicação com o cliente.

> Código numérico do status, composto por três dígitos e corresponde como nosso pedido foi condicionado no servidor.

-- **O primeiro dígito indica qual categoria ele pertence, e existem 5 categorias**.
- 1xx: Informational, significa que o pedido foi recebido e ainda está sendo processado.
- 2xx: Sucess, seu pedido foi recebido, aceito e processado com sucesso.
- 3xx: Redirection, ações adicionais precisma ser relaizada para completar seu pedido.
- 4xx: Client Error, o pedido está com infos incorretas ou não pôde ser processado.
- 5xx: Server error, servidor não conseguiu processar o pedido.

> Texto associado ao status: 
Essa descrição é destinada a ser legível por humanos e geralmente fornece mais informações sobre o resultado da requisição. No exemplo acima, a descrição é "OK", o que indica que a requisição foi bem-sucedida.

2. *Cabeçalho (header)*: semelhante ao header do request. Exemplos: Content-Type, Access-Control-Allow (indica se a resposta pode ser acessada pela origem do pedido), Date...

3. *Body (corpo)*: mensagem que o navegador vai interpretar, geralmente um html, xml, json etc.

* **Exemplo contendo linha de status, header e body**:
```
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 124

<!DOCTYPE html>
<html>
<head>
    <title>Página de Exemplo</title>
</head>
<body>
    <h1>Olá, mundo!</h1>
 <body>
</html>
```
> Com isso o navegador renderizará "Olá mundo", encerrando o ciclo http.

### Referências: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status?retiredLocale=pt-PT