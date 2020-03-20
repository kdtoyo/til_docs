
# [Ubuntu][apt] apt がロックされている場合の対処

## 

Ubuntuのapt installでLockされているとのエラーがあるが、他のプロセスで
使用していないため、何か不正な状態となっていることが考えられる。

エラーメッセージ
~~~
ubuntu:~$ sudo apt-get install xxxx
E: ロック /var/lib/dpkg/lock-frontend が取得できませんでした - open (11: リソースが一時的に利用できません)
E: Unable to acquire the dpkg frontend lock (/var/lib/dpkg/lock-frontend), is another process using it?
~~~


状態
~~~
ubuntu:~$ ls -l /var/lib/dpkg/lock*
-rw-r----- 1 root root 0 Mar 11 03:51 /var/lib/dpkg/lock
-rw-r----- 1 root root 0 Jan 22 09:36 /var/lib/dpkg/lock-frontend
~~~
0バイトとなっているので、使用するプロセスでファイルだけ作成してロックをかけているだけの単純な構成っぽい。
apt-get install中にCtrl-Cで抜けるとか、そういう心当たりがあるようなないような。。


対処
~~~
ubuntu:~$ sudo rm /var/lib/dpkg/lock
ubuntu:~$ sudo rm /var/lib/dpkg/lock-frontend 
~~~
簡単にロックファイルだけを削除。
これで通るかなと。
