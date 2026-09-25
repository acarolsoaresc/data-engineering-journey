# Evolução: integração com API externa em pipeline de dados

## Contexto

Durante o desenvolvimento de um pipeline de dados, surgiu a necessidade de consumir informações de tickets disponibilizadas por uma API externa do Help Center.

Era necessário criar uma integração que permitisse extrair os dados da API e disponibilizá-los para consumo no ambiente de dados, mantendo uma estrutura organizada e reutilizável para futuras integrações ou pipelines.

## Problema

Era necessário criar uma solução que permitisse:

- consumir dados de tickets diretamente de uma API externa;
- lidar com paginação dos resultados;
- respeitar o limite de requisições da API (rate limit);
- tratar possíveis erros durante as requisições;
- transformar os dados retornados em uma estrutura adequada para processamento;
- manter a integração desacoplada do pipeline para possibilitar reutilização;
- evitar o processamento desnecessário de dados já carregados, considerando o volume de informações da API.

## Solução desenvolvida

Foi criada uma biblioteca em Python para centralizar a integração com a API do Help Center.

A implementação foi estruturada utilizando uma classe responsável pela comunicação com a API, encapsulando configurações, autenticação, requisições e regras de extração.

A solução permitiu:

- realizar autenticação utilizando variável de ambiente;
- utilizar uma sessão HTTP para comunicação com a API;
- implementar paginação utilizando cursor;
- tratar o limite de requisições da API;
- implementar tratamento de erros HTTP e erros gerais;
- transformar dados aninhados retornados pela API em uma estrutura tabular;
- disponibilizar os dados em um DataFrame para utilização pelo pipeline;
- reutilizar a biblioteca em futuras soluções que necessitem consumir a mesma API.

O pipeline foi desenvolvido utilizando a biblioteca criada, mantendo a separação entre a integração com a API e o processamento/carga dos dados.

## Evolução da solução

Após revisão técnica da implementação, foi identificada a necessidade de transformar o processo de carga em um ETL incremental, considerando o volume de dados retornado pela API.

A solução foi ajustada para buscar e processar apenas os registros atualizados desde a última execução, evitando o processamento completo da base a cada execução.

Essa alteração tornou o processo mais eficiente e escalável, reduzindo o volume de dados processados e o tempo necessário para atualização da tabela.

## Principais aprendizados

Durante essa implementação desenvolvi conhecimentos em:

- integração com APIs externas;
- Programação Orientada a Objetos aplicada a pipelines de dados;
- criação de bibliotecas e funções reutilizáveis;
- modularização e separação de responsabilidades;
- paginação de APIs;
- tratamento de rate limit;
- tratamento de erros em requisições HTTP;
- transformação de dados JSON em estruturas tabulares;
- utilização de variáveis de ambiente para configurações sensíveis;
- implementação de ETL incremental;
- consideração de volume e escalabilidade no desenho de pipelines;
- aplicação de boas práticas de desenvolvimento em projetos de dados;
- realização de testes locais antes da disponibilização do pipeline em produção;
- evolução da solução a partir de revisão técnica e feedback.
