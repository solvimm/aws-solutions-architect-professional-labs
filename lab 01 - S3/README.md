# Lab 01 - S3

## 1.  Criação de Bucket S3

1.  Clique na aba Services e clique no serviço S3

![Image 1](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-01.png)

2.  Clique em no botão Create Bucket

![Image 2](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-02.png)

3.  Escolha um nome para o bucket e a região em que ele deve ficar. O nome do bucket deve ser único em toda a AWS, não só na sua conta.
4.  Clique no botão Next

![Image 3](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-03.png)

5.  Em "Configure options", pode-se configurar o versionamento, logs, tags, registro de atividades e criptografia do bucket. Nesse primeiro momento, não faremos essas configurações. Clique no botão Next.

![Image 4](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-04.png)

6.  Em "Set Permissions" é onde se configura as permissões de acesso ao bucket e seus objetos. Por padrão o acesso público ao bucket e seus objetos é bloqueado e é extremamente recomendado que se mantenha dessa forma. Em "Review" é possível revisar as configurações feitas nos menus anteriores. Clique em Next.

![Image 5](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-05.png)

7.  Revise as configurações e clique em Create Bucket.

![Image 6](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-06.png)

## 2.  Upload de objetos

1.  Com o bucket criado. Clique no nome do bucket para abrir as configurações

![Image 7](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-07.png)

2.  Clique na aba Overviewe clique no botão Upload

![Image 8](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-08.png)

3.  Clique no botão Add files e adicione um arquivo da sua máquina. Após adicionar o arquivo clique no botão Next.

![Image 9](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-09.png)

![Image 10](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-10.png)

4.  Em “Set permissions” podemos configurar os acessos permitidos ao objeto. Mantenha as configurações padrões e clique no botão Next.

![Image 11](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-11.png)

5.  Em “Set properties” é possível escolher em qual classe do S3 o objeto vai ser armazenado, além de configurações de criptografia e tags. Mantenha no Standard, que é o padrão, e clique no botão Next.

![Image 12](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-12.png)

6.  Em “Review” é possível revisar as configurações feitas nos menus anteriores e confirmar o upload do arquivo. Clique no botão Upload.

![Image 13](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-13.png)

## 3.  Versionamento

1.  No bucket criado anteriormente no passo 1. Clique no nome do bucket para abrir as configurações

![Image 14](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-14.png)

2.  Clique na aba Properties e clique na opção Versioning.

![Image 15](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-15.png)

3.  Clique em “Enable versioning” e clique no botão Save.

![Image 16](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-16.png)

4.  Em seguida, Faça o upload novamente do mesmo arquivo do Passo 2, seguindo os mesmos passos
5.  Após novo upload, marque a caixa de seleção do objeto e na janela que aparecer do lado direito, clique em Latest versione confirme se as duas versões do objeto estão disponíveis. É possível fazer o download de qualquer versão salva ou deletar qualquer versão.

![Image 17](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-17.png)

## 4.  Cross Region Replication

1.  No bucket criado anteriormente no passo 1. Clique no nome do bucket para abrir as configurações
2.  Clique na aba “Management”, clique no botão Replication e em seguida clique no botão Add rule

![Image 18](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-18.png)

![Image 19](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-19.png)

3.  Nessa tela, configura-se as regras de replicação, podendo selecionar todos os objetos, apenas objetos com um prefixo pré-determinado ou tag. Vamos replicar todos os objetos.
4.  Marque a opção “Entire bucket” e clique no botão Next

![Image 20](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-20.png)

5.  Em "Set destination", escolhemos um bucket já existente para replicação, ou a criação de um novo. Vamos optar por criar um novo.
6.  Também é possível definir qual a categoria de armazenamento do S3 que as réplicas serão salvas e se vamos alterar a propriedade do objeto para o proprietário do bucket de destino. Manteremos as opções padrão
7.  Com a criação do novo bucket, é necessário colocar um novo nome único e definir a região onde o bucket de replicação vai ser criado

![Image 21](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-21.png)

![Image 22](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-22.png)

8.  Após a definição do destino, precisamos dar permissão, através de IAM Role, para o bucket de origem criar um bucket de destino e fazer a cópia de arquivos nele.
9.  Clique em Select a rolee em seguida Create a new role
10.  De um nome para a regra a ser criada e clique no botão Next

![Image 23](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-23.png)

11.  Em “Review”, é possível ver as configurações feitas nos menus anteriores. Clique no botão Save.

![Image 24](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-24.png)

![Image 25](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-25.png)

12.  Após a confirmação, verifique se o bucket de destino foi criado
13.  Acesse o bucket de origem e faça o upload de um arquivo de teste

![Image 26](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-26.png)

14.  Acesse o bucket de replicação e verifique se o objeto foi replicado

![Image 27](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-27.png)

## 5.  Encriptação em repouso no S3

1.  No bucket criado anteriormente no passo 1. Clique no nome do bucket para abrir as configurações.
2.  Clique na aba Propertiese escolha a opção Default encryption

![Image 28](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-28.png)

3.  É possível escolher entre criptografar o objeto usando as chaves gerenciadas pelo Amazon S3 ou pelo KMS. Escolha a opção do gerenciamento da chave pelo S3 (AES-256) e clique no botão Save.

![Image 29](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-29.png)

## 6.  MFA Delete

1.  Para ativar o MFA Delete é necessário ter instalado o AWS CLI na máquina e a credencial da conta root
2.  Após configurado o CLI e as credenciais de acesso na máquina rodar o seguinte comando
```aws s3api put-bucket-versioning --bucket <yourbucket> --versioning-configuration Status=Enabled,MFADelete=Enabled --mfa "arn:aws:iam::<account number>:mfa/root-account-mfa-device <mfa code>"```

## 7.  Logs de acesso

1.  Crie um novo bucket seguindo o tutorial do passo 1. Esse novo bucket sera usado como bucket de destino para os logs de acesso
2.  No bucket criado anteriormente no passo 1. Clique no nome do bucket para abrir as configurações
3.  Clique na aba “Properties”, e clique na opção “Server access logging”

![Image 30](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-30.png)

4.  Clique na opção “Enable logging”. Em “Target bucket” escolha o bucket criado no passo 7.1 para ser o bucket de destino dos logs.

![Image 31](https://d2yblsmsldwfto.cloudfront.net/csap/lab01/lab-01-s3-31.png)

5.  Em “Target prefix” como opção podemos definir uma pasta para agrupar os logs que serão salvos. Vamos deixar em branco.
6.  Clique no botão Save.
7.  O registro de logs pode levar algum tempo para registrar as atividades no bucket. Crie novos arquivos no bucket principal e após algum tempo acesse o bucket de logs para confirmar a geração de logs das ações no bucket principal
