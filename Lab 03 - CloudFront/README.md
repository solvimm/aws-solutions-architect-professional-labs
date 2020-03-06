# Lab 03 - CloudFront

## 1. Fazendo Upload de uma imagem no S3

1. Abra o console do S3 em  https://s3.console.aws.amazon.com/s3/home?region=us-east-1
Clique no Bucket onde quer fazer o upload da imagem.

![Image 01](https://d1b7vbmva6nnec.cloudfront.net/lab03/lab-03-cloudfront-01.png#1)

2. Ao clicar no Bucket, escolha **Upload** para subir a imagem no S3.

![Image 02](https://d1b7vbmva6nnec.cloudfront.net/lab03/lab-03-cloudfront-02.png#1)

3. Escolha **Add files** ou arraste a imagem para fazer o Upload.

![Image 03](https://d1b7vbmva6nnec.cloudfront.net/lab03/lab-03-cloudfront-03.png#1)

4. Por fim, clique em **Upload**.
**OBS: Para poder acessar o arquivo é necessário que os objetos do bucket estejam públicos.**
Após realizar o Upload da imagem, clique no arquivo.

![Image 04](https://d1b7vbmva6nnec.cloudfront.net/lab03/lab-03-cloudfront-04.png#1)

Você será direcionado a esta página.

![Image 05](https://d1b7vbmva6nnec.cloudfront.net/lab03/lab-03-cloudfront-05.png#1)

5. Clique na **Object URL**. Ao acessar a mesma, você verá a imagem na qual fez Upload.

![Image 06](https://d1b7vbmva6nnec.cloudfront.net/lab03/lab-03-cloudfront-06.png#1)


## Criando uma Distribuição do CloudFront

1. Após realizar o Upload da Imagem no S3, abra o console do CloudFront em https://console.aws.amazon.com/cloudfront/home.
Escolha, **Create Distribution**.

![Image 07](https://d1b7vbmva6nnec.cloudfront.net/lab03/lab-03-cloudfront-07.png#1)
 
2. Existem dois tipos de distribuição, **WEB** e **RTMP**. Escolha a distribuição Web.

![Image 08](https://d1b7vbmva6nnec.cloudfront.net/lab03/lab-03-cloudfront-08.png#1)

3. O primeiro passo é especificar o Origin Domain Name. O Origin Domain Name pode ser um Bucket do S3, um Bucket do S3 configurado como site, uma instância EC2, um Load Balancer, etc. Selecione o Bucket do S3 configurado anteriormente. 

Após isso especifique o Origin Path. Se você quiser que o CloudFront solicite seu conteúdo de um diretório do seu recurso ou origem personalizada da AWS, insira o caminho do diretório começando com barra (/). O CloudFront inclui o caminho do diretório no valor de Origin Domain Name. (Campo opcional)

Em Origin ID você poderá usar o ID especificado aqui para identificar a origem ou o grupo de origens para o qual o CloudFront roteará uma solicitação quando ela tiver o mesmo caminho padrão desse comportamento de cache. Ao escolher o Origin Domain Name, automaticamente este campo é preenchido.

Em Restrict Bucket Access (Aplica-se apenas a origens do bucket do Amazon S3 ,exceto se configurado como endpoints do site). Escolha Yes (Sim) se quiser exigir que os usuários acessem objetos em um bucket do Amazon S3 usando apenas URLs do CloudFront, e não do Amazon S3. Em seguida, especifique valores adicionais. Escolha No (Não) se quiser que os usuários acessem objetos usando URLs do CloudFront ou do Amazon S3.


![Image 09](https://d1b7vbmva6nnec.cloudfront.net/lab03/lab-03-cloudfront-09.png#1)

![Image 10](https://d1b7vbmva6nnec.cloudfront.net/lab03/lab-03-cloudfront-10.png#1)

![Image 11](https://d1b7vbmva6nnec.cloudfront.net/lab03/lab-03-cloudfront-11.png#1)


4. O restante mantenha o padrão, observe que ao lado de cada recurso é possível ver uma bolinha com um “i”, ao clicar na mesma você terá informações mais detalhadas do recurso.
Por fim, clique em **Create Distribution**.

![Image 12](https://d1b7vbmva6nnec.cloudfront.net/lab03/lab-03-cloudfront-12.png#1)

5. Ao criar a distribuição, você será redirecionado para a seguinte página. Observe que o status da distribuição é “in progress”, com isso, é necessário aguardar alguns minutos para que a distribuição seja implantada.

![Image 13](https://d1b7vbmva6nnec.cloudfront.net/lab03/lab-03-cloudfront-13.png#1)

6. Após alguns minutos o status deverá ser **Deployed**.

![Image 14](https://d1b7vbmva6nnec.cloudfront.net/lab03/lab-03-cloudfront-14.png#1)

7. Copie o Domain Name no bloco de notas e retorne ao S3. Acesse o bucket criado anteriormente e copie, também, o nome da imagem. De posse do Domain name e do nome da imagem copie no navegador o Domain Name seguido do nome da imagem. 

Exemplo:
Domain Name:  d7ft7dsahus.cloudfront.net
Nome do arquivo de imagem: /logo-solvimm-nb-1.png#1

Cole no navegador: d7ft7dsahus.cloudfront.net/logo-solvimm-nb-1.png#1

8. Se todos os passos estiverem corretos, você deverá ver a imagem que está armazenada no Bucket do S3.