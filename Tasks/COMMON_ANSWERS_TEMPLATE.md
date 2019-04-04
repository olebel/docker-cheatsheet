Tasks
===
### 1. sha256 sum
```
sha256: b643c0b5f0f35c33f28e886f7ac9e359ff045b3ae0f51bb62448a2265b186336 docker
```

### 2. ubuntu
```
sha256: 865469589c2453b1da95547235c029d05b8d81782058b265c1300bae641366dc /etc/debian_version
```

### 3. centos
```
sha256: 59297533a5f227751cce6fdd6ad471f3f3631deb600d6821f02930f1e92c26fd /usr/bin/sha256sum
```

### 4. alpine
```
sudo docker run alpine wc -l /etc/passwd
28 /etc/passwd
```

### 5. busybox
```
sudo docker run busybox du -sh /
1.3M	/
```

### 6. hello-world
```
sha256: 8b6566f585bad55b6fb9efb1dc1b6532fd08bb1796b4b42a3050aacb961f1f3f  /var/lib/docker/overlay2/7fc1d0d984995ca73943164f4942c6279ede2f6d511a20c848f04bdd04e8bd7a/diff/hello
```


### 7. apache
```
root@c6b9b5676940:/usr/local/apache2# cat /etc/os-release 
PRETTY_NAME="Debian GNU/Linux 9 (stretch)"
NAME="Debian GNU/Linux"
VERSION_ID="9"
VERSION="9 (stretch)"
ID=debian
HOME_URL="https://www.debian.org/"
SUPPORT_URL="https://www.debian.org/support"
BUG_REPORT_URL="https://bugs.debian.org/"
root@c6b9b5676940:/usr/local/apache2# 

root@c6b9b5676940:~# ps aux | grep httpd
root         1  0.0  0.0  79480  4632 ?        Ss   18:30   0:00 httpd -DFOREGROUND
daemon       8  0.0  0.0 368680  3644 ?        Sl   18:30   0:00 httpd -DFOREGROUND
daemon       9  0.0  0.0 368680  3644 ?        Sl   18:30   0:00 httpd -DFOREGROUND
daemon      10  0.0  0.0 368680  3640 ?        Sl   18:30   0:00 httpd -DFOREGROUND
root       562  0.0  0.0  11112  1012 pts/0    S+   18:44   0:00 grep httpd
root@c6b9b5676940:~# 
```

### 8. compile c program
```
ubuntu sha256: 7876ecfaf87ba7855cb0299ed2ccb5e617334461346d0900effc64b0ab298b57  hello
centos sha256: 90635dcf93c75a7185bc85c4ab22f598e422fc1272ecde70fbc792edf2df59c5  hello
```
