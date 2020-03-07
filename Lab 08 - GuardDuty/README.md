# Lab 08 - GuardDuty

## Arquitetura da solução

- O GuardDuty gera um “finding” sobre alguma atividade maliciosa suspeita.
- O CloudWatch Event está configurado para disparar mediante tipos específicos de “findings” gerados pelo GuardDuty.
- Uma função Lambda é chamada pelo CloudWatch Event e analisa o finding do GuardDuty.
- Os dados de estado para hosts bloqueados são armazenados em uma tabela do Amazon DynamoDB.
- Uma segunda função Lambda verifica a tabela de estado quanto à entrada do host existente.
- A função Lambda cria uma regra no AWS WAF e em uma VPC NACL.
- Um e-mail de notificação é enviado via Amazon Simple Notification Service (SNS).

![Image 01](https://d1b7vbmva6nnec.cloudfront.net/lab08/lab-08-guardduty-01.png)

## Tipo de “findings” utilizados na configuração

- UnauthorizedAccess:EC2/SSHBruteForce
- UnauthorizedAccess:EC2/RDPBruteForce
- Recon:EC2/PortProbeUnprotectedPort
- Trojan:EC2/BlackholeTraffic
- Backdoor:EC2/XORDDOS
- UnauthorizedAccess:EC2/TorIPCaller
- Trojan:EC2/DropPoint

## 2. Deploy

1. Selecionar a região **N.Virgínia** no menu suspenso

![Image 02](https://d1b7vbmva6nnec.cloudfront.net/lab08/lab-08-guardduty-02.png)

2. Clicar na barra de busca **Find Services** e digitar **S3**

3. Clicar em Create Bucket. Preencher com os dados:
    - Bucket Name: immersion-day-si-solvimm-gd2acl-artifacts-nome-sobrenome

4. Clicar em **Create**.
![Image 03](https://d1b7vbmva6nnec.cloudfront.net/lab08/lab-08-guardduty-03.png)

5. Abrir o bucket que acabou de criar.

6. Clicar em **Upload**.

7. Clicar em **Add Files**.

8. Selecionar os 2 arquivos zip disponibilizados:
    - guardduty_to_acl_lambda.zip
    - prune_old_entries.zip

9. Clicar no menu suspenso **Services** e buscar pelo serviço **GuardDuty**.

![Image 04](https://d1b7vbmva6nnec.cloudfront.net/lab08/lab-08-guardduty-04.png)

10. Clicar em **Enable GuardDuty**.

11. Clicar no menu suspenso **Services** e buscar pelo serviço **Cloudformation**.

![Image 05](https://d1b7vbmva6nnec.cloudfront.net/lab08/lab-08-guardduty-05.png)

12. Clicar em **Create Stack**

![Image 06](https://d1b7vbmva6nnec.cloudfront.net/lab08/lab-08-guardduty-06.png)

13. Clicar em **Upload a template file** e depois em **Choose File**.

![Image 07](https://d1b7vbmva6nnec.cloudfront.net/lab08/lab-08-guardduty-07.png)

14. Selecionar o arquivo template fornecido. **aws-guardduty-acl-template**.

15. Clicar em **Next**.

16. Preencher o próximo campo com as informações abaixo:
    - Stack Name: **GuardDutytoACL**
    - Notification email (REQUIRED): **seu email**
    - Retention: **720**
    - IP Set for global CloudFront WAF: **False**
    - IP Set for regional ALB WAF: **False**
    - S3 bucket for artifacts: **immersion-day-si-solvimm-gd2acl-artifacts-nome-sobrenome**
    - S3 path to artifacts: **<VAZIO>**

17. Clicar em **Next** e na próxima tela **Next** novamente.

18. Clicar em **Create Stack**

19. Enquanto a stack estiver sendo criada, vá ao email cadastrado no campo **Notification email**, e procure por um email com o assunto **AWS Notification – Subscription Confirmation**. Entre neste email e confirme clicando no link.

![Image 08](https://d1b7vbmva6nnec.cloudfront.net/lab08/lab-08-guardduty-08.png)

## 3. Para realizar os testes

1. No painel AWS, clique em **Services > VPC > Subnets**

2. Selecione uma subnet para realizar o teste, clicando na aba Summary e copiando o Subnet-ID em um bloco de notas para usar nos próximos passos.

3. No painel AWS, clique em **Services > Cloudformation > GuardDutytoACL** stack

4. Na aba **Outputs**, procure pela Key **GuardDutytoACLLambda**

![Image 09](https://d1b7vbmva6nnec.cloudfront.net/lab08/lab-08-guardduty-09.png)

5. Clique no link para a função Lambda

![Image 10](https://d1b7vbmva6nnec.cloudfront.net/lab08/lab-08-guardduty-10.png)

6. No topo direito, clique em **Select a test event** e depois na opção **Configure test events**

![Image 11](https://d1b7vbmva6nnec.cloudfront.net/lab08/lab-08-guardduty-11.png)

7. Copie e cole o código fornecido no arquivo **teste-event.txt**

8. Altere o valor do subnetID (linha 34) com o codigo copiado na etapa 2, e clique em **Create**.

![Image 12](https://d1b7vbmva6nnec.cloudfront.net/lab08/lab-08-guardduty-12.png)

9. Clique em **Test** para executar. Voce deve receber uma mensagem `Execution result: succeeded`

![Image 13](https://d1b7vbmva6nnec.cloudfront.net/lab08/lab-08-guardduty-13.png)

10. Após executar os testes vamos confirmar os bloqueios. No painel, clique em **Services > VPC > Subnets**

11. Selecione a subnet utilizada no passo 2, na aba **Network ACL**

12. Confirme se a nova entrada foi adicionada.

![Image 14](https://d1b7vbmva6nnec.cloudfront.net/lab08/lab-08-guardduty-14.png)

## 3. AWS WAF

1. No painel, clique em **Services > WAF & Shield**, e selecione **IP Addresses**.

2. Clique em **Filtro**, selecione **Global (CloudFront)**, e depois selecione o IPSet chamado **GD2ACL CloudFront IPSet for Blacklisted IP addresses**.

![Image 15](https://d1b7vbmva6nnec.cloudfront.net/lab08/lab-08-guardduty-15.png)

3. Confirme se o IP foi adicionado a lista de IPSet

![Image 16](https://d1b7vbmva6nnec.cloudfront.net/lab08/lab-08-guardduty-16.png)

4. Clique em Filtro, selecione **US East (N. Virginia)**, e depois selecione o IPSet chamado **GD2ACL ALB IPSet for Blacklisted IP addresses**.

![Image 17](https://d1b7vbmva6nnec.cloudfront.net/lab08/lab-08-guardduty-17.png)

5. Confirme se o IP foi adicionado a lista de IPSet

6. Entre no email cadastrado para receber as notificações e verifique a mensagem recebida, com o titulo  **AWS GD2ACL Alert**.

![Image 18](https://d1b7vbmva6nnec.cloudfront.net/lab08/lab-08-guardduty-18.png)
