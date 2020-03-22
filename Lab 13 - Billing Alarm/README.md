# Lab 13 - Billing Alarm

### 1. Criação de Tag

1. Crie uma nova instancia EC2

2. Em **Instances** selecione a instancia criada e na aba **Tags** clique em **Add/Edit Tags**

![Image 01](https://d1b7vbmva6nnec.cloudfront.net/lab13/lab-13-billing-01.png)

3. Em **Add/Edit Tags** clique em **Create Tag** e em **Key** coloque ``Environment`` e **Value** coloque ``Production``. 
Clique em **Save**

![Image 02](https://d1b7vbmva6nnec.cloudfront.net/lab13/lab-13-billing-02.png)

### 2. Alocação de Tags de Custo

1. Abra o console da AWS na parte de Billing em https://console.aws.amazon.com/billing.

2. Clique em **Cost allocation tags**

![Image 03](https://d1b7vbmva6nnec.cloudfront.net/lab13/lab-13-billing-03.png)

3. Em **User-Defined Cost Allocation Tags** Selecione todas as tags e clique em **Activate** e apos a mensagem de confirmação clique novamente em **Activate**

**OBS:** As tags podem levar até 24 horas para aparecer em Billing e Cost Management 

![Image 04](https://d1b7vbmva6nnec.cloudfront.net/lab13/lab-13-billing-04.png)

### 3. Configuração de Bucket

1. Na tela de Billing clique em **Budgets**

2. Na parte superior da página, clique em **Create Budget**.

![Image 05](https://d1b7vbmva6nnec.cloudfront.net/lab13/lab-13-billing-05.png)

3. Em **Select Budget Type**, escolha **Cost Budget** (orçamento de custo).

4. Clique em **Set up your budget**.

![Image 06](https://d1b7vbmva6nnec.cloudfront.net/lab13/lab-13-billing-06.png)

5. Em **Name**, defina um nome para o orçamento de forma que fique claro o que esse orçamento significa, como, por exemplo, Budget Mensal. O nome do orçamento deve ser exclusivo na sua conta e pode usar A-Z, a-z, espaços e os seguintes caracteres: _.:/=+-%@. Em **Period**, escolha a frequência com que você deseja que o orçamento redefina o gasto previsto e real. O período pode ser Monthly (Mensal), Quarterly (Trimestral) ou Annually (Anual). 


6. Em **Budgeted Amount**, informe o valor total que você deseja gastar nesse período de orçamento. Em orçamentos de planejamento mensal e trimestral, insira o valor que você deseja gastar em cada período planejado.

![Image 07](https://d1b7vbmva6nnec.cloudfront.net/lab13/lab-13-billing-07.png)

7. Em **Budget parameters (optional)** cliquem em **Tag** e procure pela tag criada **Environment**. Selecione a tag

### 3. Configuração de Alerta
 
1. Selecione **Configure Alerts**.

2. Em Configure Alerts, para Alert 1, escolha *Actual* para criar uma notificação para gastos até o momento atual da conta e Forecast para criar uma notificação para gastos previstos no período, de acordo com o padrão de consumo até o momento. Em **Alert Threshold**, insira o valor para o qual você deseja ser notificado. Insira um valor absoluto ou uma porcentagem. Por exemplo, para um orçamento de 200 USD, se você quiser ser notificado ao atingir 160 USD (80% de seu orçamento), insira 160 para um orçamento absoluto ou 80 para uma porcentagem do orçamento.


3. Ao lado do valor, escolha *Dollar Amount* para ser notificado quando o valor limite é ultrapassado e % of budgeted amount (% do valor orçado) para ser notificado quando a porcentagem limite do orçamento é ultrapassada.


4. Em **Email Contacts**, digite os endereços de e-mail para os quais você deseja que as notificações sejam enviadas e clique em **Add email contact**. Separe vários endereços de e-mail com uma vírgula. Uma notificação pode ter até 10 endereços de e-mail.

![Image 08](https://d1b7vbmva6nnec.cloudfront.net/lab13/lab-13-billing-08.png)


5. Clique em **Confirm Budget**.

6. Revise as configurações do orçamento e clique em **Create**.