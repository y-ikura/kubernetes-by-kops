# 参考

# kopsのインストール
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
4. 

