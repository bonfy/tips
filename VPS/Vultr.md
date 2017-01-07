## Vultr配置

用过一阵子Digital Ocean， 总感觉速度有点不给力，听说Vultr 稳定、速度、优惠多，所以百闻不如一试，自己搞了个试了下

### 关于优惠

优惠还是蛮多的，我入的时候正逢 新用户 送50美元（60days过期）， 不过这个必须绑定信用卡，而且银联的还不行，最后只能忍痛绑定了paypal,送5美元

### 关于服务器选择

网上的言论主要集中于 LA or Tokyo 之间的选择，Tokyo 可能快一点，也有可能从美国绕，据说LA不丢包，所以我只试了下LA的，ping 大概在300ms 好的时候 180ms，丢包还行，可以忍受。

最近新开了 新加坡节点 , 没试过不清楚速度怎样，而且以后有机会也想试试 Tokyo的


### 关于配置

5dollar/month 一档的， Server 选择Ubuntu， 那个SSH key其实不用填，我填了，没啥用，后面会说怎么配置，其实参考[vultr无密钥登陆](http://www.jianshu.com/p/460b4ce4f8e1)就行，直接将本机的 .ssh/id_rsa.pub 拷贝到服务器的 .ssh文件夹下并重命名为 authorized_keys就行

### 关于文件传输

用 scp 命令

```cmd
$ scp username@servername:/path/filename /tmp/local_destination # 从服务器下载文件
$ scp /path/local_filename username@servername:/path            # 上传本地文件到服务器
$ scp -r username@servername:remote_dir/ /tmp/local_dir         # 从服务器下载整个目录
$ scp  -r /tmp/local_dir username@servername:remote_dir         # 上传目录到服务器
```

### 关于安装nginx

```cmd
$ sudo apt-get update
$ sudo apt-get install nginx
```

nginx 装好就启动了， 占了80端口

nginx 的目录 在 /etc/nginx

nginx.conf 中的一行是  ： include sites-enabled/*

sites-enabled里面有default 配置了初始版本的 index.html地址

然后 /var/www/html 里面有默认页面

### 参考

* [vultr 1月优惠](http://www.cnvultr.com/255.html)
* [vultr 搭建SS](https://www.91ssfq.com/archives/123)
* [How to Setup Gunicorn to Serve Python Web Applications](https://www.vultr.com/docs/how-to-setup-gunicorn-to-serve-python-web-applications)
* [vultr无密钥登陆](http://www.jianshu.com/p/460b4ce4f8e1)
* [scp](http://www.runoob.com/linux/linux-comm-scp.html)
