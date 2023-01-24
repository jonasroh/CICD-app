DEPLOY DE UMA APLICAÇÃO JAVA NO ELASTIC BEANSTALK

Essa aplicação irá expor uma API que permite visualizar ou remover carros de uma database

BUILDANDO A APLICAÇÃO
Nessa primeira etapa foi criado um arquivo.gitlab-yml para a criação de uma pipeline. No estágio de build são gerados artefatos. 

SMOKE TEST
O smoke test é um teste bem simples para testar se algo está funcionando
Nesse teste iremos chamar um endpoint. Um Curl será usado para ver se a aplicação responde.

Para isso, iremos subir a aplicação através do artefato gerado no stage anterior. Como a aplicação demora um pouco para inicializar foi adicionado um sleep de 30 segundos e então o script executa o curl e verifica se existe o status "UP". 

Agora iremos fazer o deploy da apicação no Elastic Beanstalk.
- Primeiramente é preciso criar um bucket no S3 para armazenar o artefato gerado no build.
- O nome do bucket foi adicionado como variável no gitlab
- Credenciais também foram adicionados como variáveis
Deploy
A imagem usada já possui o AWS CLI. Foi definido também que não deve haver nenhum entrypoint. Os comando executados pelo script são para simplesmente copiar o artefact para o bucket criado anteriormente.