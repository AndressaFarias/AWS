**Scenario 1:** 
Crie uma outra conta na AWS, acessando sua conta principal no menu My Organization, através da segunda opção Create account.

   > 


**Scenario 2:** 
Agora, crie uma outra conta usando a opção _Invite account_.
Para isso, você precisar criar essa conta antes. 
No total do dia, você precisa ter 3 contas criadas na AWS, na seguinte estrutura:

   >  sreandressafariasdev@gmail.com

**Organização das contas:**

Master Account/Payer Account
    1 OU: Dev
      Dev Account
    1 OU: Prod
      Prod Account
      
**Na conta de Dev, os usuarios não devem conseguir criar RDS**

    ~~~json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
            "Sid": "Statement1",
            "Effect": "Deny",
            "Action": [
                "rds:*"
            ],
            "Resource": [
                "*"
            ]
            }
        ]
    }
    ~~~


**Na conta de Prod, os usuarios não devem conseguir criar S3**

    ~~~json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
            "Sid": "Statement1",
            "Effect": "Deny",
            "Action": [
                "s3:*"
            ],
            "Resource": [
                "*"
            ]
            }
        ]
    }
    ~~~


**Simule o uso dessas SCP em cada conta, usando outros browsers para poder logar em multiplas contas ao mesmo tempo.**
Ex.: Chrome para logar na Master Account, Firefox para logar na conta Dev com o Root(email da conta) e Modo Anônimo do firefox ou do Chrome para logar na conta de Prod com o Root(email da conta);

Obs: Use SCP para definir essas regra e attach em cada conta sua respectiva SCP.

Tentativa de criar RDS na conta de Dev

~~~json
   User: arn:aws:iam::xxx:root is not authorized to perform: rds:DescribeDBEngineVersions with an explicit deny in a service control policy (Service: AmazonRDS; Status Code: 403; Error Code: AccessDenied; Request ID: f81e4576-862d-48d8-bcf8-c5cd3dac4659; Proxy: null) 
~~~

Ao acessar página para criar um S3 na conta Prod

~~~json
Você não tem permissões para listar buckets
Atualize esta página depois que você ou o administrador da AWS tiver atualizado suas permissões para permitir a ação s3:ListAllMyBuckets. Saiba mais sobre o Identity and Access Management no Amazon S3 
~~~