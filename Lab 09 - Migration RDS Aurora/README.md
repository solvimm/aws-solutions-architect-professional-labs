# Lab 09 - Migration RDS Aurora

## 1. Criação do RDS

1. Acesse o painel do RDS digitando `rds` em **Find Services**.

![Image 01](https://d1b7vbmva6nnec.cloudfront.net/lab09/lab-09-migration-01.png)

2. Clique em **Create database**.

![Image 02](https://d1b7vbmva6nnec.cloudfront.net/lab09/lab-09-migration-02.png)

3. Em **Choose a database creation method** escolha a opção **Easy Create**.

4. Em **Configuration** escolha **MySQL**.

![Image 03](https://d1b7vbmva6nnec.cloudfront.net/lab09/lab-09-migration-03.png)

5. Em **DB instance size** escolha a opção **Free tier**. 

6. Em **DB instance identifier** digite um nome para a instancia RDS.

7. Marque a opção **Auto generate a password**.

8. Mantenha o restantes das configurações e clique em **Create database**.

![Image 04](https://d1b7vbmva6nnec.cloudfront.net/lab09/lab-09-migration-04.png)

9. A pagina voltara para a tela de **Databases**, mostrando a criação da instancia.

![Image 05](https://d1b7vbmva6nnec.cloudfront.net/lab09/lab-09-migration-05.png)

10. Para visualizar a senha de acesso ao banco clique em **View credential details**.

![Image 06](https://d1b7vbmva6nnec.cloudfront.net/lab09/lab-09-migration-06.png)

## 2. Criação do Aurora read replica

1. Apos a instancia entrar em status **Available** clique na instancia criada e em **Modify** clique em **Create Aurora read replica**

![Image 07](https://d1b7vbmva6nnec.cloudfront.net/lab09/lab-09-migration-07.png)

2. Em **DB engine version** escolha a ultima versão disponivel.

3. Em **DB instance class** escolha **db.t2.small**

4. Em **Multi-AZ deployment** escolha **Create Replica in Different Zone**

![Image 08](https://d1b7vbmva6nnec.cloudfront.net/lab09/lab-09-migration-08.png)

5. Em **DB instance identifier** digite um nome para a instancia Aurora RDS.

6. Mantenha o restantes das configurações e clique em **Create read replica**.

![Image 09](https://d1b7vbmva6nnec.cloudfront.net/lab09/lab-09-migration-09.png)

![Image 10](https://d1b7vbmva6nnec.cloudfront.net/lab09/lab-09-migration-10.png)

7. A pagina voltara para a tela de **Databases**, mostrando a criação das instancias Aurora.

![Image 11](https://d1b7vbmva6nnec.cloudfront.net/lab09/lab-09-migration-11.png)

## 2. Migração para o Aurora

1. Apos as instancias entrar em status **Available** clique na instancia Aurora criada e em **Action** clique em **Promote**

![Image 12](https://d1b7vbmva6nnec.cloudfront.net/lab09/lab-09-migration-12.png)

2. Clique em **Promote Read Replica**

![Image 13](https://d1b7vbmva6nnec.cloudfront.net/lab09/lab-09-migration-13.png)