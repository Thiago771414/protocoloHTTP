# Protocolo HTTP
O Protocolo de Transferência de Hipertexto (HTTP) é um protocolo de comunicação utilizado para transferir dados na World Wide Web (WWW). Ele define a estrutura das mensagens e o comportamento do cliente e servidor para realizar requisições e obter respostas. Neste resumo, vamos aprender sobre os principais elementos do HTTP, incluindo linhas da requisição, linhas de cabeçalho, linha de resposta, corpo da entidade (payload), códigos de retorno, métodos e Content-Type MIME.

## Requisição HTTP
Uma requisição HTTP é feita pelo cliente para o servidor e possui a seguinte estrutura:
````javascript
MÉTODO URL VERSÃO_HTTP
Cabeçalho1: Valor1
Cabeçalho2: Valor2
...
CabeçalhoN: ValorN

Corpo da Requisição (Payload)
````
MÉTODO: Indica a ação que o cliente deseja executar no servidor, como GET (obter dados), POST (enviar dados), PUT (atualizar dados) ou DELETE (excluir dados).

URL: É o endereço do recurso que o cliente deseja acessar.

VERSÃO_HTTP: Indica a versão do protocolo HTTP utilizada, como HTTP/1.1 ou HTTP/2.

Cabeçalhos: São linhas opcionais que contêm informações adicionais sobre a requisição, como Accept (tipos de conteúdo aceitos), Authorization (autenticação), Accept-Encoding (tipos de compressão aceitos) e outros.

Corpo da Requisição (Payload): É uma seção opcional que pode conter dados a serem enviados ao servidor, geralmente utilizado em requisições POST ou PUT.

## Resposta HTTP
Uma resposta HTTP é enviada pelo servidor para o cliente e possui a seguinte estrutura:
````javascript
VERSÃO_HTTP CÓDIGO_DE_RETORNO TEXTO_DO_STATUS
Cabeçalho1: Valor1
Cabeçalho2: Valor2
...
CabeçalhoN: ValorN

Corpo da Resposta (Payload)
````
VERSÃO_HTTP: Indica a versão do protocolo HTTP utilizada, como HTTP/1.1 ou HTTP/2.

CÓDIGO_DE_RETORNO: É um número de três dígitos que indica o resultado da requisição. Por exemplo, 200 significa "OK" (sucesso), 404 significa "Not Found" (recurso não encontrado) e 500 significa "Internal Server Error" (erro interno do servidor).

TEXTO_DO_STATUS: É uma breve descrição do código de retorno, explicando o resultado da requisição.

Cabeçalhos: São linhas opcionais que contêm informações adicionais sobre a resposta, como Content-Type (tipo de conteúdo), Content-Length (tamanho do corpo da resposta), e outros.

Corpo da Resposta (Payload): É uma seção opcional que contém os dados enviados pelo servidor como resposta à requisição.

## Content-Type MIME
O Content-Type MIME é um cabeçalho que especifica o tipo de dados que está sendo enviado no corpo da requisição ou resposta. Alguns dos valores mais comuns são:

image: Para representar imagens.
text: Para representar texto.
application: Para representar arquivos binários ou outros tipos de dados genéricos.

## Exemplo de Requisição HTTP em JavaScript
Aqui está um exemplo de como fazer uma requisição HTTP utilizando JavaScript e definindo alguns cabeçalhos:
````javascript
// Importar a biblioteca "http" do Node.js
const http = require('http');

// Configurar as informações da requisição
const options = {
  hostname: 'www.exemplo.com',
  path: '/recurso',
  method: 'GET',
  headers: {
    'Accept': 'application/json', // Indica que aceitamos dados no formato JSON
    'Authorization': 'Bearer seu_token_de_autenticação',
    'Accept-Encoding': 'gzip', // Indica que aceitamos resposta comprimida com gzip
  }
};

// Realizar a requisição HTTP
const req = http.request(options, (res) => {
  // Aqui você pode tratar a resposta do servidor
  console.log(`Código de Retorno: ${res.statusCode}`);
  console.log(`Cabeçalhos: ${JSON.stringify(res.headers)}`);

  res.on('data', (chunk) => {
    console.log(`Dados Recebidos: ${chunk}`);
  });
});

// Tratar erros na requisição
req.on('error', (error) => {
  console.error(`Erro na Requisição: ${error.message}`);
});

// Finalizar a requisição
req.end();
````
