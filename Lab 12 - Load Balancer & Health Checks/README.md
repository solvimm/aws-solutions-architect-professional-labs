# Lab 12 - Load Balancer & Health Checks


## 1. Criação de EC2

1.  Acesse o console de EC2 e crie 2 EC2 em zonas de disponibilidade distintas.

## 2. Criação de Target Group

1. Após a criação dos dois servidores, no painel da EC2, selecione **Target Groups** no menu da esquerda. Em seguida, clique em **Create Target Group**.

![Image 01](https://d1b7vbmva6nnec.cloudfront.net/lab12/lab-12-loadbalancer-01.png)

2. Nas configurações, insira o nome do target group (Solvimm-Group), em **Target type** selecione ```Instance```, em **Protocol** selecione ```HTTP```, em **Port** selecione ```80```, e em **VPC** selecione a ```Default```. 

![Image 02](https://d1b7vbmva6nnec.cloudfront.net/lab12/lab-12-loadbalancer-02.png)

3. Em **Health check settings** selecione **Protocol** como ```HTTP``` e o **Path** como ```/index.html```.

4. Em Advanced health check settings, siga as configurações da figura abaixo. Por fim, clique em **Create**.

![Image 03](https://d1b7vbmva6nnec.cloudfront.net/lab12/lab-12-loadbalancer-03.png)


5. Selecione o Target Group criado e no campo **Targets** clique em **Edit**.

![Image 04](https://d1b7vbmva6nnec.cloudfront.net/lab12/lab-12-loadbalancer-04.png)

6. Selecione as duas instâncias criadas anteriormente clique em **Add to registered**. Por fim, clique em **Save**.


## 3. Criação do Application Load Balancer


1. No console da EC2, selecione **Load Balancer** no menu da esquerda e, em seguida, clique em **Create Load Balancer**.


![Image 05](https://d1b7vbmva6nnec.cloudfront.net/lab12/lab-12-loadbalancer-05.png)

2. Clique em **Create** em Application Load Balancer.

![Image 06](https://d1b7vbmva6nnec.cloudfront.net/lab12/lab-12-loadbalancer-06.png)

3. Na página Configure Load Balancer, vamos inserir o Nome ```Solvimm-Labs-ALB```, o Scheme será ```internet-facing```, e o IP address type será ```ipv4```. 

4. Em Listeners, vamos utilizar o protocolo ```HTTP``` na porta ```80```.

5. No campo Availability Zones, especifique a VPC, bem como as AZs que o Load Balancer irá utilizar.

6. Clique em **Next: Configure Security Settings**.

![Image 07](https://d1b7vbmva6nnec.cloudfront.net/lab12/lab-12-loadbalancer-07.png)

![Image 08](https://d1b7vbmva6nnec.cloudfront.net/lab12/lab-12-loadbalancer-08.png)

7. Em Configure Security Groups, selecione um Security Group para o Load Balancer e clique em **Next: Configure Routing**.

![Image 09](https://d1b7vbmva6nnec.cloudfront.net/lab12/lab-12-loadbalancer-09.png)

8. Em **Configure Routing**, selecione o Target Group criado anteriormente e clique em **Next: Register Targets**.

![Image 10](https://d1b7vbmva6nnec.cloudfront.net/lab12/lab-12-loadbalancer-10.png)

9. Em Register Targets, clique em **Next: Review** e, em seguida, clique em **Create**.

![Image 11](https://d1b7vbmva6nnec.cloudfront.net/lab12/lab-12-loadbalancer-11.png)

![Image 12](https://d1b7vbmva6nnec.cloudfront.net/lab12/lab-12-loadbalancer-12.png)

