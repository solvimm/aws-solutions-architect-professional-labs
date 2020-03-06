# Lab 11 - Networking


## 1. Fazendo o setup do ambiente

1. Na aba de região, selecione uma região que não tenha nenhum recurso, isso facilitará o desnevolvimento desse Lab (ex: ca-central-1).
2. Primeiro, abra o console da AWS e entre no serviço do **CloudFormation**.

![Image 1](../img/011-01.png)

3. Clique em **Create stack** para subir o CloudFormation.
4. Na *Prepare template*, selecione **Template is ready**. Em *Specify template*, selecione **Upload a template file**. Depois disso clique no botão **Choose file**. Depois de ter feito o upload do arquivo **01-setup.yml**, clique em **Next**.

![Image 2](../img/011-02.png)

5. Em *Stack name*, coloque um nome para sua stack (por exemplo: Solvimm-ASAP-Networking-Lab-Setup). Mantenha o restante das opções e clique em **Next**.

![Image 3](../img/011-03.png)

6. Na aba *Configure stack options*, clique em **Next**.
7. Na aba *Review*, clique em **Create stack** para fazer o deploy do CloudFormation.
8. Aguarde alguns minutos (cerca de 5 minutos), até o status da stack ficar como **CREATE_COMPLETE**.

![Image 4](../img/011-04.png)

9. Para testar o ambiente criado, no **nome da stack** e depois vá na aba **Outputs**. Copie o **Value** do *output* que tem como key *FQDN* (será algo parecido com ec2-52-60-200-253.ca-central-1.compute.amazonaws.com)

![Image 5](../img/011-05.png)

10. Cole no navegador o valor copiado no passo **9** para testar o ambiente. O resultado deverá ser como o da imagem abaixo:

![Image 6](../img/011-06.png)

## 2. Criando o desastre

1. Para criar o desastre no seu ambiente, selecione sua stack clique em **Update**.
2. Na aba *Update stack*, selecione **Replace current template**. Em *Specify template*, selecione **Upload a template file**. Depois disso clique no botão **Choose file**. Depois de ter feito o upload do arquivo **03-disaster.yml**, clique em **Next**.
3. Na aba *Specify stack details*, clique em **Next**.
4. Na aba *Configure stack options*, clique em **Next**.
5. Na aba *Review*, clique em **Update stack**.
6. Aguarde alguns minutos (cerca de 5 minutos), até o status da stack ficar como **UPDATE_COMPLETE**. 
7. Teste novamente o url recuperado no passo **8** da primeira parte, e verifique se seu ambiente ficou fora do ar.

![Image 7](../img/011-07.png)

## 3. Desafio

 - Sem olhar os arquivos do CloudFormation e sem executar o change set, faça uma investigação no seu ambiente, pelo console, para descobrir o que aconteceu no seu ambiente. **Seu desafio é recuperar o ambiente**.

 ## 4. Limpando o ambiente

 - Para limpar o ambiente, selecione a stack criada e clique em **Delete**. No pop-up de confirmação, confirme clicando em **Delete stack**.
 