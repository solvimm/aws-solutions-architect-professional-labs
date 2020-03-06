# Lab 04 - VPC

## 1. Criação de VPC

1. Faça login no console da AWS e acesso o serviço Amazon VPC em: https://console.aws.amazon.com/vpc/.

2. No canto superior direito do console, escolha a região na qual deseja criar a sua VPC.

3. Para começar a criar uma VPC, clique em **Launch VPC Wizard**.

4. Na página **Step 1: Select a VPC Configuration**, escolha **VPC with Public and Private Subnets (VPC com sub-redes públicas e privadas)** e depois clique em **Select**.

![Image 01](https://d1b7vbmva6nnec.cloudfront.net/lab04/lab-04-vpc-01.png)

5. Na página **Step 2: VPC with Public and Private Subnets**, defina estes valores:
    - IPv4 CIDR block: **10.0.0.0/16**
    - IPv6 CIDR block: nenhum bloco CIDR IPv6
    - VPC name: **tutorial-vpc**
    - Public subnet's IPv4 CIDR: **10.0.0.0/24**
    - Availability Zone: **us-west-2a**
    - Public subnet name: **Tutorial public**
    - Private subnet's IPv4 CIDR: **10.0.1.0/24**
    - Availability Zone: **us-west-2a**
    - Private subnet name: **Tutorial Private 1**
    - Service endpoints: ignore este campo
    - Enable DNS hostnames: **Yes**
    - Hardware tenancy: **Default**

![Image 02](https://d1b7vbmva6nnec.cloudfront.net/lab04/lab-04-vpc-02.png)

6. Ao terminar as configurações, clique em **Create VPC**

## 2 Criação de Subnet

1. Para criar uma subnet adicional, acesso novamente pelo console a página da Amazon VPC.

2. Para adicionar a segunda subnet privada à VPC, escolha **Subnets** e **Create subnet**.

![Image 03](https://d1b7vbmva6nnec.cloudfront.net/lab04/lab-04-vpc-03.png)

3. Na página **Create Subnet**, defina esses valores:

    - Name tag: **Tutorial private 2**
    - VPC: escolha a VPC que você criou na etapa anterior, por exemplo: **vpc-identifier (10.0.0.0/16) | tutorial-vpc**
    - Availability Zone: **us-west-2b**
    - Escolha uma Zona de disponibilidade que é diferente da que você escolheu para a primeira sub-rede privada.
    - IPv4 CIDR block: **10.0.2.0/24**

![Image 04](https://d1b7vbmva6nnec.cloudfront.net/lab04/lab-04-vpc-04.png)

4. Quando terminar, clique em **Create**. Em seguida, clique em **Close** na página de confirmação.

5. Para garantir que a segunda subnet privada que você criou use a mesma tabela de rotas que a primeira, clique em **Subnets** e escolha a primeira subnet privada que você criou para a VPC, **Tutorial private 1**.

6. Abaixo da lista de subnets, selecione a guia Route Table, e observe o valor de Route Table, por exemplo, rtb-55d5082b.

![Image 05](https://d1b7vbmva6nnec.cloudfront.net/lab04/lab-04-vpc-05.png)

7. Na lista de subnets, escolha a segunda subnet privada **Tutorial private 2** e depois escolha a guia **Route Table**.

8. Se a tabela de rotas atual não for a mesma que a tabela de rotas da primeira subnet privada, escolha **Edit route table association**. Em **Route Table ID**, escolha a tabela de rotas que você anotou antes, por exemplo: rtb-55d5082b. Em seguida, para salvar a seleção, clique em **Save**.

## 3 Criação de Security Group

1. Para criar um security group de VPC, acesse o dashboard inicial de VPC, selecione no menu da esquerda **Security Groups** e clique em **Create security group**.

2. Na página de criação de SG, defina os valores:
    - Security group name (Nome do grupo de segurança): tutorial-securitygroup
    - Description (Descrição): Tutorial Security Group
    - VPC: escolha a VPC criada anteriormente, por exemplo: vpc-identifier (10.0.0.0/16) | tutorial-vpc

![Image 06](https://d1b7vbmva6nnec.cloudfront.net/lab04/lab-04-vpc-06.png)

3. Clique em **Create**.

4. Vá até o SG criado e clique na guia **Inbound Rules** e clique em **Edit rules**.

![Image 07](https://d1b7vbmva6nnec.cloudfront.net/lab04/lab-04-vpc-07.png)

5. Adicione uma regra de acesso SSH para o seu IP e clique em **Save**

## 4 VPC Flow Logs

1. Para iniciar o VPC Flow Logs, é necessário fazer a criação de um grupo de Flow Logs no Amazon CloudWatch. Vá no menu de serviços e acesse o CloudWatch.

2. Na página inicial do CloudWatch, utilize o menu ao lado esquerdo e clique em **Logs**.

3. Na página de Logs, clique em **Actions** e clique em **Create log group**

![Image 08](https://d1b7vbmva6nnec.cloudfront.net/lab04/lab-04-vpc-08.png)

4. Defina um nome para o grupo e finalize a criação.

5. Após ter o grupo de logs criado, acesse o menu de serviços e clique em **VPC**.

6. Na página inicial de VPC, acesse em **Your VPCs** no menu da esquerda para poder visualizar todas as VPCs criadas e escolher a VPC que deseja criar o Flow Logs.

7. Selecione a VPC e clique em **Actions** e, em seguida, clique em **Create flow** para iniciar a configuração do seu VPC Flow Logs Group.

![Image 09](https://d1b7vbmva6nnec.cloudfront.net/lab04/lab-04-vpc-09.png)

8. Na página de criação, altere o filter para **All** e deixe o **Destination** enviando os logs para o CloudWatch.

9. No **Destination log group**, selecione o Flow Logs Group criado anteriormente no CloudWatch e clique em **Set Up Permissions** para criar a IAM Role que vai permitir a VPC escrever os Logs no CloudWatch.

![Image 10](https://d1b7vbmva6nnec.cloudfront.net/lab04/lab-04-vpc-10.png)

10. Uma nova janela vai ser aberta para configuração da IAM Role, escolha um nome e clique em permitir. Após permitir, volte a página de configuração do VPC Flow Logs.

![Image 11](https://d1b7vbmva6nnec.cloudfront.net/lab04/lab-04-vpc-11.png)

11. Clique na seta de atualização do IAM Role e selecione a IAM Role criada no passo anterior e, em seguida, clique em **Create** para finalizar.

![Image 12](https://d1b7vbmva6nnec.cloudfront.net/lab04/lab-04-vpc-12.png)

12. Para visualizar os logs, selecione a VPC onde o Flow Log foi criado e vá no menu Flow logs.

13. Clique no Destination name que está em azul para ir direto ao Flow Log Group. Você chegará na página para olhar os logs.

![Image 13](https://d1b7vbmva6nnec.cloudfront.net/lab04/lab-04-vpc-13.png)

## 5 VPC Endpoints

1. Para criar um VPC Endpoint para o S3, abra o console de Amazon VPC em https://console.aws.amazon.com/vpc/.

2. Na coluna lateral, clique em **Endpoints**. Em seguida, clique em **Create Endpoint**.

![Image 14](https://d1b7vbmva6nnec.cloudfront.net/lab04/lab-04-vpc-14.png)

3. Na etapa seguinte, mantenha a opção **Service category** marcada como **AWS services**.

![Image 15](https://d1b7vbmva6nnec.cloudfront.net/lab04/lab-04-vpc-15.png)

4. Na opção **Service Name**, selecione o serviço S3.

![Image 16](https://d1b7vbmva6nnec.cloudfront.net/lab04/lab-04-vpc-16.png)

5. Abaixo, na opção **VPC**, clique no menu e selecione o **vpc-id** correspondente a sua VPC

![Image 17](https://d1b7vbmva6nnec.cloudfront.net/lab04/lab-04-vpc-17.png)

6. Na opção **Configure route tables**, selecione as route tables que receberão as rotas para o VPC Endpoint.

![Image 18](https://d1b7vbmva6nnec.cloudfront.net/lab04/lab-04-vpc-18.png)

7. Na opção **Policy**, mantenha selecionado **Full Access**. Clique em **Create Endpoint**.

![Image 19](https://d1b7vbmva6nnec.cloudfront.net/lab04/lab-04-vpc-19.png)

8. Após este passo, você receberá um aviso confirmando a criação do endpoint. Clique em **Close**.

![Image 20](https://d1b7vbmva6nnec.cloudfront.net/lab04/lab-04-vpc-20.png)

9. Verifique se o endpoint é exibido no painel.

![Image 21](https://d1b7vbmva6nnec.cloudfront.net/lab04/lab-04-vpc-21.png)

10. Após alguns minutos, verifique se a rota foi inserida na route table corretamente.
Para isso, entre no painel de **Route Tables**, selecione a tabela de rotas, e clique na aba Routes. Se tudo estiver correto, deve existir uma linha contendo a regra de roteamento, com Target para o id do VPC Endpoint (vpce-xxxxxxxxxxx) criado.

![Image 22](https://d1b7vbmva6nnec.cloudfront.net/lab04/lab-04-vpc-22.png)