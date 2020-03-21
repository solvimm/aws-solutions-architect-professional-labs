# Lab 11 - Auto Scaling

## 1. Criação do Launch Configuration

1. Entre no console da AWS e na aba de Serviços escolha o serviço EC2

2. Clique em **Launch Configuration**

![Image 01](https://d1b7vbmva6nnec.cloudfront.net/lab11/lab11-autoscaling-01.png)

3. Clique em **Create launch Configuration**

![Image 02](https://d1b7vbmva6nnec.cloudfront.net/lab11/lab11-autoscaling-02.png)

3. Escolha a AMI **Amazon Linux 2 AMI (HVM)** e clique em **Select**

![Image 03](https://d1b7vbmva6nnec.cloudfront.net/lab11/lab11-autoscaling-03.png)

4. Escolha a instancia **m5.large** e clique em **Next: Configure details**

![Image 04](https://d1b7vbmva6nnec.cloudfront.net/lab11/lab11-autoscaling-04.png)

5. Em **Name** digite um nome para o Launch Configuration

6. Em **Purchasing option** marque a opção **Request Spot Instances**

7. Em **Maximum price** digite o preço corrente da instancia Spot

8. Em **Monitoring** marque a opção **Enable CloudWatch detailed monitoring**

![Image 05](https://d1b7vbmva6nnec.cloudfront.net/lab11/lab11-autoscaling-05.png)

9. Na aba **Advanced Details** em **User data** preencha com o script
    ```
    #!/bin/bash
    yum update -y
    yum install stress -y
    /usr/bin/stress --cpu 8 --timeout 10m
    ```
10. Em **IP Address Type** escolha a opção **Do not assign a public IP address to any instance**

11. Clique em **Skip to review**

![Image 06](https://d1b7vbmva6nnec.cloudfront.net/lab11/lab11-autoscaling-06.png)

12. Clique em **Create launch configuration**

![Image 07](https://d1b7vbmva6nnec.cloudfront.net/lab11/lab11-autoscaling-07.png)

13. Escolha a opção **Proceed without a key pair** e marque a opção **I acknowledge that I will not be able to connect to this instance unless I already know the password built into this AMI.** clique em **Create launch configuration**

![Image 08](https://d1b7vbmva6nnec.cloudfront.net/lab11/lab11-autoscaling-08.png)

## 2. Criação do Auto Scaling Group

1. Selecione o Launch Configuration criado e Clique em **Create Auto Scaling Group**

![Image 09](https://d1b7vbmva6nnec.cloudfront.net/lab11/lab11-autoscaling-09.png)

2. Em **Group Name** defina um nome para o Auto Scaling Group

3. Em **Network** escolha a VPC onde o Auto Scaling vai atuar

4. Em **Subnet** escolha as subnets associadas a VPC

![Image 10](https://d1b7vbmva6nnec.cloudfront.net/lab11/lab11-autoscaling-10.png)

5. Na aba **Advanced Details** em **Health Check Grace Period** digite 60 segundos

6. Em **Monitoring** Marque a opção **Enable CloudWatch detailed monitoring**

7. Clique em **Next: Configure next scaling policies**

![Image 11](https://d1b7vbmva6nnec.cloudfront.net/lab11/lab11-autoscaling-11.png)

8. Escolha a opção **Use scaling policies to adjust the capacity of this group**

9. Digite 1 e 3 Na frase **Scale between and instances**

10. No **Scale Group Size** em **Target value** digite 60

11. Em **Instances need** digite 60

12. Clique em **Review**

![Image 12](https://d1b7vbmva6nnec.cloudfront.net/lab11/lab11-autoscaling-12.png)

13. Defina uma **Key** e um **Value** para tags e clique em **Review**

![Image 13](https://d1b7vbmva6nnec.cloudfront.net/lab11/lab11-autoscaling-13.png)

14. Clique em **Create Auto Scaling group**

![Image 14](https://d1b7vbmva6nnec.cloudfront.net/lab11/lab11-autoscaling-14.png)

## 2. Execução do Auto Scaling Group

1. Selecione o Auto Scaling Group configurado e em **Actions** escolha **Edit**

![Image 15](https://d1b7vbmva6nnec.cloudfront.net/lab11/lab11-autoscaling-15.png)

2. Em **Default Cooldown** digite 60 e clique em **Save**

![Image 16](https://d1b7vbmva6nnec.cloudfront.net/lab11/lab11-autoscaling-16.png)

3. Em **Instances** confirme a execução de uma instancia rodando

![Image 17](https://d1b7vbmva6nnec.cloudfront.net/lab11/lab11-autoscaling-17.png)

4. Volte para Auto Scaling Groups, selecione o Auto Scaling Group configurado e em **Actions** escolha **Edit**

![Image 18](https://d1b7vbmva6nnec.cloudfront.net/lab11/lab11-autoscaling-18.png)

5. Em **Desired Capacity** aumente para 2 e clique em **Save**

![Image 19](https://d1b7vbmva6nnec.cloudfront.net/lab11/lab11-autoscaling-19.png)

6. Na aba **Instances** verifique a nova instancia sendo criada

![Image 20](https://d1b7vbmva6nnec.cloudfront.net/lab11/lab11-autoscaling-20.png)