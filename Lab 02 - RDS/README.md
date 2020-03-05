# Lab 02 - RDS


## 1. Criação de RDS

1. Acesse o dashboard do RDS e clique em **Create database**.

![Image 01](https://d1b7vbmva6nnec.cloudfront.net/lab02/lab-02-rds-01.png)

2. Em **Choose a database creation method**, selecione a opção **Standard create**.

![Image 02](https://d1b7vbmva6nnec.cloudfront.net/lab02/lab-02-rds-02.png)

3. Escolha a Engine do RDS. Para o Lab escolhemos Aurora. Em edição, selecione **Amazon Aurora with MySQL compatibility**. Em database location, selecione **Regional**.

![Image 03](https://d1b7vbmva6nnec.cloudfront.net/lab02/lab-02-rds-03.png)

4. Em **Database features**, selecione **One writer with multiple readers**.

![Image 04](https://d1b7vbmva6nnec.cloudfront.net/lab02/lab-02-rds-04.png)

5. Em **Templates**, selecione **Production**.

![Image 05](https://d1b7vbmva6nnec.cloudfront.net/lab02/lab-02-rds-05.png)

6. Em **Settings*, defina um nome para o seu banco de dados. Configura também as credenciais.

![Image 06](https://d1b7vbmva6nnec.cloudfront.net/lab02/lab-02-rds-06.png)

7. Em **DB instance size**, para esse lab, selecione a opção **Bustable classes**, pois possui configurações com menor custo. Selecione a **db.t2.small **.

![Image 07](https://d1b7vbmva6nnec.cloudfront.net/lab02/lab-02-rds-07.png)

8. Em **Availability and durability**, selecione **Don't create and Aurora replica**. Faremos isso em outro lab.

![Image 08](https://d1b7vbmva6nnec.cloudfront.net/lab02/lab-02-rds-08.png)

9. Por fim, deixe as configurações de rede e VPC padrões e clique em **Create database**.

![Image 09](https://d1b7vbmva6nnec.cloudfront.net/lab02/lab-02-rds-09.png)

10. De volta à tela inicial do RDS, poderá ver o banco de dados recém criado.

![Image 10](https://d1b7vbmva6nnec.cloudfront.net/lab02/lab-02-rds-10.png)


## 2. Configuração de RDS Multi-AZ

1. Acesse o dashboard do RDS para encontrar o cluster RDS Aurora criado no Lab 12. Note que no cluster criado há apenas uma instância e veja em qual AZ está situada. No print deste exemplo, vemos que foi criado na AZ ```us-east-1d```.

 
2. Selecione o cluster criado, clique em **Actions** e, em seguida, selecione a opção **Add reader**.


![Image 11](https://d1b7vbmva6nnec.cloudfront.net/lab02/lab-02-rds-11.png)

3. Selecione também uma instância ```db.t2.small``` e, em **Network & Security**, selecione uma zona de disponibilidade diferente da utilizada pela primeira instância do cluster. Neste caso, selecionamos ```us-east-1c```.

![Image 12](https://d1b7vbmva6nnec.cloudfront.net/lab02/lab-02-rds-12.png)


4. Em **Settings**, insira um **DB instance identifier** para identificar a instância criada.

![Image 13](https://d1b7vbmva6nnec.cloudfront.net/lab02/lab-02-rds-13.png)


5. Em **Monitoring**, habilite a função **Enable enhanced monitoring**.


6. Deixe as outras configurações com o padrão e clique em **Add reader**.


7. Após a criação, o cluster do RDS agora é Multi-AZ


## 3. Autoscaling de réplicas de leitura


1. Para habilitar autoscaling de réplicas de leitura no Amazon Aurora, é necessário selecionar o cluster, clicar em Actions e escolher **Add replica auto scaling**.

![Image 14](https://d1b7vbmva6nnec.cloudfront.net/lab02/lab-02-rds-14.png)


2. Determine a **Policy name**, a Target metric e Target Value. Neste lab, vamos definir a regra de escala para *Average CPU utilization of Aurora Replicas* acima de 70%,

![Image 15](https://d1b7vbmva6nnec.cloudfront.net/lab02/lab-02-rds-15.png)


3. Em **Cluster capacity details**, vamos definir sempre um mínimo de 2 réplicas de leitura e um máximo de 4.

![Image 16](https://d1b7vbmva6nnec.cloudfront.net/lab02/lab-02-rds-16.png)

4. Clique em **Add policy** para finalizar.


5. Como a regra criada exige sempre um mínimo de duas réplicas de leitura, clique no botão de refresh na tela principal do RDS e, dentro de instantes, poderá observar uma réplica sendo criada automaticamente pela regra do autoscaling.


## 4. Backup Automático

1. Para habilitar o backup automático, selecione o cluster e clique em **Modify **.

2. Faça o scroll até a seção **Backup**.

3. Nessa seção, poderemos configurar o período de retenção (1 dia por default) e a janela de execução. Neste lab, vamos definir um período de retenção de 30 dias o início às 03h00 UTC.

![Image 17](https://d1b7vbmva6nnec.cloudfront.net/lab02/lab-02-rds-17.png)

4. Clique em **Continue**. Em seguida, valide as configurações e clique em **Modify cluster** para aplicar as modificações.
