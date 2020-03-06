# Lab 05 - Route 53 Routing Policy

Para este Lab, será necessário criar préviamente os seguintes recursos:
- 1 VPC em N. Virginia (us-east-1) com DNS ativado (CIDR: 172.31.0.0/16).
- 1 Subnet com o mesmo CIDR da VPC criada em Virginia.
- 1 VPC em Frankfurt (eu-central-1) com DNS ativado (CIDR: 172.32.0.0/16).
- 1 Subnet com o mesmo CIDR da VPC criada em Frankfurt.
- 1 VPC-Peering entre a vpc criada em Virginia e a criada em Frankfurt.
- Rota para ambas VPCs pelo peering criado.
- 2 EC2 com Elastic IP em Virginia (Bastion-us, Server-us)
- 2 EC2 com Elastic IP em Frankfurt (Bastion-eu, Server-eu)
- Security Groups das EC2 com inbound All Traffic para 0.0.0.0/0
- 1 Health-Check simples apontando para https://solvimm.com:443 retornando status Healthy

## 1. Criar Hosted Zone Privada

1. Acesse o painel de Hosted Zones no Route 53: https://console.aws.amazon.com/route53/home?region=us-east-1#hosted-zones:

2. Para criar uma private hosted zone, clique em **Create Hosted Zone**.

![Image 01](https://d1b7vbmva6nnec.cloudfront.net/lab05/lab-05-route53-01.png)

3. Em seguida, preencha os campos abaixo:
    - Domain: **solvimm.lab**
    - Comment: **DEIXE EM BRANCO**
    - Type: **Private Hosted Zone for Amazon VPC**
    - VPC ID: **ESCOLHA O ID DA VPC DE US EAST (N. VIRGINIA)**

4. Clique em **Create**

![Image 02](https://d1b7vbmva6nnec.cloudfront.net/lab05/lab-05-route53-02.png)

5. Após criar, clique em **Back to Hosted Zone**

6. Selecione a hosted zone **solvimm.lab**, clicando no marcador circular ao lado do nome.

7. No menu do lado direito, clique novamente no campo **VPC ID** e adicione a VPC criada em Frankfurt.

8. Clique em **Associate New VPC**

## 2. Criar Hosted Zone Privada

1. Entre na hosted zone **solvimm.lab** e clique em Create Record Set e preencha os campos conforme figura abaixo, adicionando no campo Value o Elastic IP da EC2 de Virginia. Mantenha a opção Routing Policy como **Simple** e clique em **Create**.

![Image 03](https://d1b7vbmva6nnec.cloudfront.net/lab05/lab-05-route53-03.png)

2. Repita o processo anterior, desta vez alterando os valores referentes a região de Frankfurt, conforme figura abaixo.

![Image 04](https://d1b7vbmva6nnec.cloudfront.net/lab05/lab-05-route53-04.png)

3. Acesse a EC2 Bastion-us, via ssh, e verifique o retorno do comando: `nslookup us-east-1.solvimm.lab`

4. Acesse a EC2 Bastion-eu, via ssh, e verifique o retorno do comando: `nslookup eu-central-1.solvimm.lab`

## 3. Geolocation Routing Policy

1. Entre na Hosted Zone **solvimm.lab** e clique em **Create Record Set** e preencha os campos abaixo:
    - Name: **geo**
    - Type: **CNAME**
    - Value: **us-east-1.solvimm.lab**
    - Routing Policy: **Geolocation**
    - Location: **North America**
    - Set ID: **north-america**
    - Associate with Health Check: **No**

![Image 05](https://d1b7vbmva6nnec.cloudfront.net/lab05/lab-05-route53-05.png)

2. Repita o processo anterior, alterando os valores:
    - Value: **eu-central-1.solvimm.lab**
    - Location: **Default**
    - Set ID: **everywhere**

![Image 06](https://d1b7vbmva6nnec.cloudfront.net/lab05/lab-05-route53-06.png)

3. Acesse a EC2 Bastion-us, via ssh, e verifique o retorno do comando: `nslookup geo.solvimm.lab`

4. Acesse a EC2 Bastion-eu, via ssh, e verifique o retorno do comando: `nslookup geo.solvimm.lab`

## 4. Latency Routing Policy

1. Entre na hosted zone solvimm.lab e clique em Create Record Set e preencha os campos abaixo:
    - Name: **latency**
    - Type: **CNAME**
    - Value: **us-east-1.solvimm.lab**
    - Routing Policy: **Latency**
    - Region: **us-east-1**
    - Set ID: **eua**
    - Associate with Health Check: **No**

![Image 07](https://d1b7vbmva6nnec.cloudfront.net/lab05/lab-05-route53-07.png)

2. Repita o processo anterior, alterando os valores:
    - Value: **eu-central-1.solvimm.lab**
    - Region: **eu-central-1**
    - Set ID: **europa**

![Image 08](https://d1b7vbmva6nnec.cloudfront.net/lab05/lab-05-route53-08.png)

3. Acesse a EC2 Bastion-us, via ssh, e verifique o retorno do comando: `nslookup geo.solvimm.lab`

4. Acesse a EC2 Bastion-eu, via ssh, e verifique o retorno do comando: `nslookup geo.solvimm.lab`

## 5. Failover Routing Policy

1. Entre na Hosted Zone **solvimm.lab** e edit o record set **us-east-1.solvimm.lab**

2. Altere as opções:
    - Routing Policy: **Failover**
    - Failover Record Type: **Primary**
    - Set ID: **us-east-1-primary**
    - Associate with Health Check: **Yes**
    - Selecione o health-check criado anteriormente.

![Image 09](https://d1b7vbmva6nnec.cloudfront.net/lab05/lab-05-route53-09.png)

3. Repita o processo anterior, editando o record set **eu-central-1.solvimm.lab** Altere as opções:
    - Name: **us-east-1**
    - Routing Policy: **Failover**
    - Failover Record Type: **Secondary**
    - Set ID: **us-east-1-secondary**
    - Associate with Health Check: **No**

![Image 10](https://d1b7vbmva6nnec.cloudfront.net/lab05/lab-05-route53-10.png)

4. Acesse a EC2 Bastion-us, via ssh, e verifique o retorno do comando: `nslookup us-east-1.solvimm.lab` 
Deverá retornar o IP do Server1-us

5. Vamos simular uma falha no health-check, forçando ele a ficar unhealthy, selecionando a opção **Invert health check status** no **Advanced Configuration**

![Image 11](https://d1b7vbmva6nnec.cloudfront.net/lab05/lab-05-route53-11.png)

6. Acesse a EC2 Bastion-us, via ssh, e verifique o retorno do comando: `nslookup us-east-1.solvimm.lab` Deverá retornar o IP do Server1-eu

