## 参考
[kopsを使ったAWS上でのKubernetesのインストール](https://kubernetes.io/ja/docs/setup/production-environment/tools/kops/)

[kopsを使ってKubernetesクラスタをAWS上で構成](https://aws.amazon.https://kubernetes.io/ja/docs/setup/production-environment/tools/kops/com/jp/blogs/news/configure-kubernetes-cluster-on-aws-by-kops/)

## 環境
* Master Node * 1台
    * RHEL t2.medium
* Worker Node * 1台
    * RHEL 

## kopsのインストール
  1. kops をリリースページからダウンロードする</dt>
```
curl -LO https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64

[ec2-user@ip-172-31-23-20 ~]$ ls -l
-rw-rw-r--. 1 ec2-user ec2-user 165171007 Mar 25 12:50 kops-linux-amd64
```

2. 実行権限を付与
```
[ec2-user@ip-172-31-23-20 ~]$ chmod +x kops-linux-amd64
[ec2-user@ip-172-31-23-20 ~]$ ls -l kops-linux-amd64
-rwxrwxr-x. 1 ec2-user ec2-user 165171007 Mar 25 12:50 kops-linux-amd64
```
3. PATHの配下へ移動
```
[ec2-user@ip-172-31-23-20 ~]$ sudo mv kops-linux-amd64 /usr/local/bin/kops
```
4. SSH鍵を生成
```
[ec2-user@ip-172-31-23-20 ~]$ ls .ssh/
authorized_keys
[ec2-user@ip-172-31-23-20 ~]$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/ec2-user/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ec2-user/.ssh/id_rsa.
Your public key has been saved in /home/ec2-user/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:7BQuaCImHdxbdO72+B/Tl8+Cv5ewyvnbj0S/RuD1cvQ ec2-user@ip-172-31-23-20.ap-northeast-1.compute.internal
The key's randomart image is:
+---[RSA 3072]----+
|      . .        |
| . . . o         |
|  o . . o        |
| . . + + .   . ..|
|o.o + . S   . +.o|
|o. o   = o   =.oE|
|        o . o.*++|
|         .. o=o*+|
|          .=++**=|
+----[SHA256]-----+
[ec2-user@ip-172-31-23-20 ~]$ ls .ssh/
authorized_keys  id_rsa  id_rsa.pub
```
5. aws cliのインストールと初期設定
    
    5.1 Python 3 および pip ツールをインストール
    ```
    [ec2-user@ip-172-31-23-20 ~]$ sudo yum install python3
    ```

    5.2 pip コマンドを使用して、AWS コマンドラインツール をインストール
    
    * awscliインストール
    ```
    [ec2-user@ip-172-31-23-20 ~]$ sudo pip3 install awscli
    ```
    
    * AWS CLI をインストールできたことを確認
    ```
    [ec2-user@ip-172-31-23-20 ~]$  aws --version
    aws-cli/1.22.82 Python/3.6.8 Linux/4.18.0-348.12.2.el8_5.x86_64 botocore/1.24.27
    ```
    
    5.3 アクセスキーの作成
        [IAM ユーザーのアクセスキーの管理](https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/id_credentials_access-keys.html)
    * アクセスキーを作成するためのポリシーを作成
    今回は「CreateOwnAccessKeys」というポリシーを作成しました。
    ```
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "CreateOwnAccessKeys",
                "Effect": "Allow",
                "Action": [
                    "iam:CreateAccessKey",
                    "iam:GetUser",
                    "iam:ListAccessKeys"
                ],
                "Resource": "arn:aws:iam::*:user/${aws:username}"
            }
        ]
    }
    ```

    * 作成したポリシーをアタッチ
    ![CreateOwnAccessKeysのアタッチ](https://user-images.githubusercontent.com/95552593/160240611-7a22f8bf-02e6-425b-9dee-881c8fe49a53.png)
    
    * アクセスキーの作成
    ![アクセスキーの作成](https://user-images.githubusercontent.com/95552593/160240924-6f9ac34c-6a8c-4882-9e28-43cb5e62ef4e.png)



    
6. AWS CLIを実行するユーザ(ローカル環境)に、以下のポリシーを持っていることを確認する:
```
AmazonEC2FullAccess
AmazonRoute53FullAccess
AmazonS3FullAccess
IAMFullAccess
AmazonVPCFullAccess
```

    今回は「AdministratorAccess」ポリシーを付与しています。
    ![AdministratorAccess](https://user-images.githubusercontent.com/95552593/160238956-1931be5f-0cd0-4622-921d-ec9de67e9505.png) 
    
7. kops用のS3バケットの作成
8. 

