# 安装

参考:[Debian GNU and Ubuntu: Setting up MIT Kerberos 5](http://techpubs.spinlocksolutions.com/dklar/kerberos.html)

## 步骤

```
sudo apt-get install krb5-{admin-server,kdc}
```

```
Default Kerberos version 5 realm? LANJING.COM
# (Your domain name in uppercase - a standard for naming Kerberos realms)

Add locations of default Kerberos servers to /etc/krb5.conf? Yes
# (Adding entries to krb.conf instead of DNS, for simplicity)

Kerberos servers for your realm: vm3.lanjing.com
# (Make sure your DNS resolves vm3.lanjing.com to
# the NETWORK IP of the server, NOT 127.0.0.1!). Hint is given in
# the section called “Conventions”.

Administrative server for your Kerberos realm: vm3.lanjing.com
# (Make sure your DNS resolves vm3.lanjing.com to
# the NETWORK IP of the server, NOT 127.0.0.1!). Same hint as above.

Create the Kerberos KDC configuration automatically? Yes

Run the Kerberos V5 administration daemon (kadmind)? Yes
```
As soon as the installation is done, the Kerberos admin server (kadmind) and the KDC will start. Kadmind will fail as, initially, there are no Kerberos realms created, which is fine.

```
sudo krb5_newrealm
```
编辑  /etc/krb5.conf，在[domain_realm]下增加realm定义:

```
.lanjing.com=LANJING.COM
lanjing.com=LANJING.COM
```
在该文件的底部添加如下内容
```
[logging]
	kdc = FILE:/var/log/kerberos/krb5kdc.log
	admin_server = FILE:/var/log/kerberos/kadmin.log
	default = FILE:/var/log/kerberos/krb5lib.log
```

建立log目录并设置权限
```
sudo mkdir /var/log/kerberos
sudo touch /var/log/kerberos/{krb5kdc,kadmin,krb5lib}.log
sudo chmod -R 750  /var/log/kerberos
```
使配置生效
```
sudo invoke-rc.d krb5-admin-server restart
sudo invoke-rc.d krb5-kdc restart
```
## 测试

### kadmin.local

## 注意事项