# Usar api online
para usar a api basta acessar a url http://shorturl.somee.com/
com os seguinte complementos:
    http://shorturl.somee.com/api/URLs/{parametro de quantidade}/maisacessadas -- retorno as urls mais acessadas
    http://shorturl.somee.com/api/URLs?alias={somealias} -- retorna informações da url a partir do alias
    method post -- http://shorturl.somee.com/api/URLs?alias={alias}&url={url} -- cadastra a url e gera uma shorturl (o alias é opcional)
    http://shorturl.somee.com/api/URLs/lotobr/ir -- se o alias existir o cliente é redirecionado para url 

os testes para o serviço foram feitos usando o Postman.

#### -----------------------------------------
    
# Hire.me
Um pequeno projeto para testar suas habilidades como programador.

## Instruções Gerais

1. *Clone* este repositório
2. Em seu *fork*, atenda os casos de usos especificados e se desejar também os bonus points
3. Envio um e-mail para c0606585@vale.com com a seu Nome e endereço do repositorio.

## Projeto

O projeto consiste em reproduzir um encurtador de URL's (apenas sua API), simples e com poucas funções, porém com espaço suficiente para mostrar toda a gama de desenho de soluções, escolha de componentes, mapeamento ORM, uso de bibliotecas de terceiros, uso de GIT e criatividade.

O projeto consiste de dois casos de uso: 

1. Shorten URL
2. Retrieve URL

### 1 - Shorten URL
![Short URL](http://i.imgur.com/MFB7VP4.jpg)

1. Usuario chama a API passando a URL que deseja encurtar e um parametro opcional **CUSTOM_ALIAS**
    1. Caso o **CUSTOM_ALIAS** já exista, um erro especifico ```{ERR_CODE: 001, Description:CUSTOM ALIAS ALREADY EXISTS}``` deve ser retornado.
    2. Toda URL criada sem um **CUSTOM_ALIAS** deve ser reduzida a um novo alias, **você deve sugerir um algoritmo para isto e o porquê.**
    
2. O Registro é colocado em um repositório (*Data Store*)
3. É retornado para o cliente um resultado que contenha a URL encurtada e outros detalhes como
    1. Quanto tempo a operação levou
    2. URL Original

Exemplos (Você não precisa seguir este formato):

* Chamada sem CUSTOM_ALIAS
```
PUT http://shortener/create?url=http://www.vale.com.br

{
   "alias": "XYhakp",
   "url": "http://shortener/u/XYhakp",
   "statistics": {
       "time_taken": "10ms",
   }
}
```

* Chamada com CUSTOM_ALIAS
```
PUT http://shortener/create?url=http://www.vale.com.br&CUSTOM_ALIAS=vale

{
   "alias": "vale",
   "url": "http://shortener/u/vale",
   "statistics": {
       "time_taken": "12ms",
   }
}
```

* Chamada com CUSTOM_ALIAS que já existe
```
PUT http://shortener/create?url=http://www.github.com&CUSTOM_ALIAS=vale

{
   "alias": "vale",
   "err_code": "001",
   "description": "CUSTOM ALIAS ALREADY EXISTS"
}
```

### 2 - Retrieve URL
![Retrieve URL](http://i.imgur.com/f9HESb7.jpg)

1. Usuario chama a API passando a URL que deseja acessar
    1. Caso a **URL** não exista, um erro especifico ```{ERR_CODE: 002, Description:SHORTENED URL NOT FOUND}``` deve ser retornado.
2. O Registro é lido de um repositório (*Data Store*)
3. Esta tupla ou registro é mapeado para uma entidade de seu projeto
3. É retornado para o cliente um resultado que contenha a URL final, a qual ele deve ser redirecionado automaticamente

## Stack Tecnológico

Não há requerimentos específicos para linguagens, somos poliglotas. Utilize a linguagem que você se sente mais confortável.

## Bonus Points

1. Crie *testcases* para todas as funcionalidades criadas
2. Crie um *endpoint* que mostre as dez *URL's* mais acessadas 
3. Crie um *client* para chamar sua API
4. Faça um diagrama de sequencia da implementação feita nos casos de uso (Dica, use o https://www.websequencediagrams.com/)
5. Monte um deploy da sua solução utilizando containers
6. Monte uma estrategia para analise dos logs em series de tempo
7. Crie sua infra de forma automatica (https://www.chef.io/ , https://www.ansible.com/ https://www.terraform.io/)
