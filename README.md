# Pipeline de implantação de API Java

Projeto desenvolvido para implantação de uma pipeline CI/CD simples no Elastic Beanstalk da AWS. A código utilizado nesse projeto é uma aplicação java bem simples de gerenciamento de frota de carros.

## 📁 Acesso ao projeto

Você pode acessar ao código inicial do projeto aqui: https://gitlab.com/gitlab-course-public/cars-api

## Pré-requisitos

- GitLab CI/CD configurado e habilitado para o repositório
- Variáveis de ambiente configuradas (por exemplo, as credenciais da AWS)
- Criar manualmente um bucket no S3 e também uma aplicação no Elastic Beanstalk, assim como o ambiente da aplicação.

## Uma breve visão sobre o .gitlab-cy.yml

Essa pipeline é composta por 3 estágios, são eles: Build, Teste e Deploy. O *Build* é responsável por complicar o código da API, o *Teste* é para realizar todos os verificar se tudo está funcionando normalmente e o *Deploy* é a fase final do pipeline responsável por colocar a aplicação em produção.
 
- Build: Nesse estágio foi executado um comando através do gradle para complicar o código-fonte da API.
- smoke test: Nesse job é ralizado uma chamada para um endpoint através de um curl para verificar de forma bem simples se a API responde.
- code quality: Nesse job é verificado a qualidade do código. O PMD é uma das ferramentas existente que servem a esse propósito. O que estamos interessados em obter são os reports gerados por essa ferramenta.
- unit test: Outro teste utilizado foi o unit test. Esses tipos de teste são geralmente escritos pelo próprio desenvolvedor para detectar erros de programação e garantir a qualidade do código.
- deploy: Nese job é onde é realizado o deploy da aplicação. De forma resumida o que é feito aqui é copiar o build do código para um bucket do S3 e depois copiar essa build do S3 para o elastic beanstalk. Uma verificação bem simples também é realizada para garantir que tudo ocorreu corretamente.

Esse pipeline ainda possui espaços para muitos apriromantes. Como por exemplo, um staging test, que permite a criacão de um ambiente apropiado para teste, antes que de fato a aplicação entre em produção.
