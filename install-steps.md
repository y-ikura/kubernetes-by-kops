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
5. aws cliをインストール

6. 

