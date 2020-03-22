# Lab 14 - Zero Downtime Deployment


## 1. Blue-green deployment

### Parte 1

1. Abra o console da AWS e vá para o **Elastic Beanstalk**.

2. Na parte superior direita da página, clique em **Create New Application**, dê um nome para a nova aplicação e clique em **Create**.

3. Dentro da aplicação criada, devemos criar um novo environment. No centro da tela deve aparecer uma mensagem "No environments currently exist for this application. Create one now.", clique em **Create one now.**.

4. Na criação do environment, escolha **Web servr environment**  e clique em **Select**; na próma página, coloce o **Environment name** como "<NOME_DO_SEU_ENVIRONMENT>"; no **Domain**, coloque o mesmo nome do seu environment; Em **Base configuration**, escolha **Node.js** em Plarform; Por fim, em **Application code**, selecione **Upload your code**, clique no botão ***Upload** e faça o upload do aquivo **v1.zip** (contido nessa pasta); Ao final, clique em **Create enviroment**.

5. Aguarde cerca de 5 minutos para seu environment terminar de ser criado.

6. Quando for criado, clique no nome do seu ambiente que você ierá para uma tela como essa: ![Image 01](https://d1b7vbmva6nnec.cloudfront.net/lab14/01.png)
   
7. Clique no URL na parte superior da tela, você deve ir para uma página e receber a seguinte mensagem de resposta: `{"hostname":"<HOST>,"version":1,"msg":"**Solvimm ASAP - v1**","uuid4":"<UUID4>"}`.
   
### Parte 2

1. Vamos criar a segunda versão do ambiente como um clone do primeiro e trocar o código para a versão atualizada do código. Para isso, clique em **Actions** > **Clone environment**.

2. Troque "-1" para **-v2** em **Environment name** e em **Environment URL**, então clique em **Clone**.

3. Aguarde cerca de 5 minutos para seu environment terminar de ser clonado. Quano terminar, clique no nome do seu ambiente para ter a visão dos dois ambientes. Espera até ambos ficarem verdes (Heath status: OK)

![Image 02](https://d1b7vbmva6nnec.cloudfront.net/lab14/02.png)

4. Agora vamos adicionar a segunda versão da aplicação. No canto superior esquerdo, clique no nome do seu environment e depois **Application Versions**. Clique em **Upload** no canto direito. Coloque **v2** como nome do *Version label*. Em *Upload aplication*, clique em **Choose File** e faça o upload do **v2.zip**, ao final, clique e **Upload**.

5. Para fazer o deploy da segunda versão, selecione **v2**, clique em **Actions** > **Deploy**. No pop-up, selecione seu ambiente com final **v2** e clique em **Deploy**.

6. Aguarde cerca de 2 minutos para o termino do deploy (Você pode acompanhar clicando no link **events page** que aparecerá).

7. Clique em **Environments** para voltar a tela anterior.

8. Para testar o Zero Downtime Deployment, vamos utilizar o comando `watch -n 1 curl -s <URL>`. Esse comando roda a cada 1 segundo, executando o comando *curl* para chamar a URL da aplicação.

9.  Abra o terminal com e rode o comando com a URL do seu primeiro ambiente. ex: `watch -n 1 curl -s solvimm-asap.us-east-2.elasticbeanstalk.com` e acompanhe o terminal rodando.

10. Ainda no Console da AWS, clique em **All aplications**
![Image 03](https://d1b7vbmva6nnec.cloudfront.net/lab14/03.png)

11. Clique em **Swap URLs**. e troque o ambiente atual pelo ambiente com final **-v2**


12. Espere a troca das URLs, como imagens abaixo. Essa troca é feita no **Route53** e demora alguns minutos para ser realizada.
![Image 04](https://d1b7vbmva6nnec.cloudfront.net/lab14/04.png)
![Image 05](https://d1b7vbmva6nnec.cloudfront.net/lab14/05.png)

13. Após alguns minutos o terminal (rodando o comando watch) vai atualizar para a nova versão, sem downtime. (resultado esperado na nova versão `{"hostname":"<HOST>,"version":2,"msg":"**Solvimm ASAP - v2**","uuid4":"<UUID4>","now":"<DATA_ATUAL>"}`).
