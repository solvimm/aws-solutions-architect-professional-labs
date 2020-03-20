# Lab 24 - Serverless Website

## 1. Criação de Função Lambda

1. Entre no console da AWS e na aba de Serviços escolha o serviço Lambda. Clique em **Create a function**.

![Image 01](https://d1b7vbmva6nnec.cloudfront.net/lab10/lab-10-serverless-01.png)

2. Na opção **Author from scratch** digite o nome **MyFirstLambdaFunction** como nome da função. No campo **Runtime** escolha **Python 3.7**.

![Image 01](https://d1b7vbmva6nnec.cloudfront.net/lab10/lab-10-serverless-02.png)

3. No campo **Permissions** clique na seta ao lado de **Choose or create an execution role**. No campo **Execution role**, escolha a opção **Create a new role from AWS policy templates**.

4.  No campo **Role name**, digite o nome **MyLambdaExecutionRole**.


5. No campo **Policy templates**, escolha a opção **Simple microservice permissions**. Clique no botão **Create a function**

![Image 01](https://d1b7vbmva6nnec.cloudfront.net/lab10/lab-10-serverless-03.png)

6. Em function code, copie e cole o código abaixo:

```
def lambda_handler(event, context):
    print("In lambda handler")

    response = {
        'statusCode': 200,
        'headers': {
            'Access-Control-Allow-Origin': '*'
        },
        'body': 'Criando um Site Web Serverless'
    }
    
    return response
```

7. Clique em **Save**.

![Image 01](https://d1b7vbmva6nnec.cloudfront.net/lab10/lab-10-serverless-04.png)


## 2. Configuração de API Gateway

1. Clique no botão **Add Trigger** e em **Trigger configuration** escolha a opção **API Gateway**.

![Image 01](https://d1b7vbmva6nnec.cloudfront.net/lab10/lab-10-serverless-05.png)

2. Em **Security** escolha a opção **AWS IAM** e clique no botão **Add**.

![Image 01](https://d1b7vbmva6nnec.cloudfront.net/lab10/lab-10-serverless-06.png)

3. Em **API Gateway** clique no nome **MyFirstLambdaFunction-API**.

![Image 01](https://d1b7vbmva6nnec.cloudfront.net/lab10/lab-10-serverless-07.png)

4. Em **Resources**, abaixo de **/MyFirstLambdaFunction**, selecione **ANY** e no botão **Actions** escolha a opção **Delete Method** para excluir o método já criado.

![Image 01](https://d1b7vbmva6nnec.cloudfront.net/lab10/lab-10-serverless-08.png)

5. Em **Resources**, clique no botão **Actions** escolha a opção **Create Method**. Escolha a opção **GET** e confirme.

![Image 01](https://d1b7vbmva6nnec.cloudfront.net/lab10/lab-10-serverless-09.png)

6. Selecione **GET**. Marque a opção **Use Lambda Proxy integration**. Em **Lambda Function** digite o nome **MyFirstLambdaFunction**. Clique no botão **Save**.

![Image 01](https://d1b7vbmva6nnec.cloudfront.net/lab10/lab-10-serverless-10.png)

7. Em **Add Permission to Lambda Function** clique no botão **OK**.

8. Em **Resources** no botão **Actions** escolha a opção **Deploy API**.


## 3. Validação de Integração Lambda e API Gateway

1. Em **Stages**, clique na seta ao lado do criado anteriormente (default) e selecione **GET**. Em **Invoke URL**, clique na url.

![Image 01](https://d1b7vbmva6nnec.cloudfront.net/lab10/lab-10-serverless-11.png)

2. Confirme o aparecimento da mensagem **Criando um site Web Serverless**.

![Image 01](https://d1b7vbmva6nnec.cloudfront.net/lab10/lab-10-serverless-12.png)


## 4. Configuração de S3 para hospedar site estático

1. Crie um arquivo com o nome **index.html** e copie e cole o código abaixo:

OBS: onde está escrito "YOUR-API-GATEWAY-LINK-HERE" substitua pela url mostrada em **Invoke URL**.

```
<html>
<script>

function myFunction() {
    var xhttp = new XMLHttpRequest();
    xhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
        document.getElementById("my-demo").innerHTML = this.responseText;
        }
    };
    xhttp.open("GET", "YOUR-API-GATEWAY-LINK-HERE", true);
    xhttp.send();

}

</script>
<body><div align="center"><br><br><br><br>
<h1>Bem vindo <span id="my-demo">Aluno</span></h1>
<button onclick="myFunction()">Me clique</button><br>
<img src="https://solvimm.com/wp-content/uploads/2019/07/logo-solvimm-e1562258364688.png"></div>
</body>
</html>
```

2. Acesse o serviço S3 e crie um bucket

3. Selecione o bucket criado e clique no botão **Edit public access settings**

4. Desmarque a opção **Block all public access** e clique no botão **Save**.

5. Clique na aba **Properties** e na opção **Static website hosting**.

![Image 01](https://d1b7vbmva6nnec.cloudfront.net/lab10/lab-10-serverless-13.png)

6. Selecione a opção **Use this bucket to host website** e defina tanto o **Index document** quanto o **Error document** como **"index.html**. Clique no botão **Save**.

7. Faça o upload do arquivo index.html criado para o bucket. Ao finalizar, selecione o mesmo, clique em **Actions** e, em seguida, clique no botão **Make public**.

8. Retorne para **Static website hosting** e copie a URL para acessar o site estático.

9. Confirme o aparecimento do site e se o botão está funcionando corretamente.

![Image 01](https://d1b7vbmva6nnec.cloudfront.net/lab10/lab-10-serverless-14.png)