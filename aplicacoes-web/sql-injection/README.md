# SQL Injection

### O que é?

SQL Injection é uma vulnerabilidade de aplicações web que permite a manipulação das queries sql que serão feitas diretamente no banco de dados através da aplicação. A exploração desta vulnerabilidade pode permitir o acesso a dados sensíveis da aplicação, como dados de acesso e informações dos usuários.

![imagem sql injection](./imgs/sql-injection.svg)


### Requisitos

É importante saber como realizar as operações básicas de sql e como funciona o protocolo Http e seus métodos de requisição.

[Requisições Http - MDN Web Docs](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods)

[SQL Para Iniciantes - DevMedia](https://www.devmedia.com.br/sql-select-guia-para-iniciantes/29530)


### Exemplos

#### Dados Ocultos

Vamos supor que uma página de venda de produto possua uma url que realize um GET passando o id de um produto como parametro para realizar a consulta no banco.

_Requisição da aplicação:_ 

```
https://www.meusiteficticio.com.br/produtos.php?id=10
```
_Query Sql:_

```
SELECT * FROM produtos WHERE id_produto = ${id} 
```

Repare que o id é inserido no final da query sql e caso a aplicação não trate esta consulta da maneira correta é possível concatenar outras queries sql conseguindo assim dados ocultos da aplicação.

Vamos tentar conseguir que a alpicação nos liste todos os produtos que existem no banco de dados:

```
 https://www.meusiteficticio.com.br/produtos.php?id=10' OR 1 = 1 --

```

Inserindo este comando sql no final da url estamos concatenando a query que está pronta na aplicação. O resultado seria este:

```
SELECT * FROM produtos WHERE id_produto = ${id} OR 1 = 1
```

Desta forma temos acesso a detalhes de produtos que não estão disponíveis na aplicação.

#### Manipulando a Lógica da Aplicação

Vamos supor que na página de de login a aplicação possui dois `<input>` para login e senha e ao fazer a requisição de login a aplicação monte a seguinte query sql: 

```
SELECT * FROM usuarios WHERE username = 'nomedousuario' AND password = 'senhadousuario'
```
> Ou seja, o banco de dados irá retornar o usuário caso ele encontre um usuário com o login e senha informados

É possível utilizarmos o `--` para comentar todo o restante da query. Passando o nome de usuário `nomedousuario' --` não importa a senha que você passar pois tudo que está a direita será apenas um comentŕaio. Sendo assim a validação seria somente no username e a query ficaria assim:

```
SELECT * FROM usuarios WHERE username = nomedousuario -- AND password = blablabla
```




