# 安装

参考:[Debian GNU and Ubuntu: Setting up MIT Kerberos 5](http://techpubs.spinlocksolutions.com/dklar/kerberos.html)

## 步骤

```
sudo apt-get install krb5-{admin-server,kdc}
```

```
Default Kerberos version 5 realm? SPINLOCK.HR
# (Your domain name in uppercase - a standard for naming Kerberos realms)

Add locations of default Kerberos servers to /etc/krb5.conf? Yes
# (Adding entries to krb.conf instead of DNS, for simplicity)

Kerberos servers for your realm: krb1.spinlock.hr
# (Make sure your DNS resolves krb1.spinlock.hr to
# the NETWORK IP of the server, NOT 127.0.0.1!). Hint is given in
# the section called “Conventions”.

Administrative server for your Kerberos realm: krb1.spinlock.hr
# (Make sure your DNS resolves krb1.spinlock.hr to
# the NETWORK IP of the server, NOT 127.0.0.1!). Same hint as above.

Create the Kerberos KDC configuration automatically? Yes

Run the Kerberos V5 administration daemon (kadmind)? Yes
```
As soon as the installation is done, the Kerberos admin server (kadmind) and the KDC will start. Kadmind will fail as, initially, there are no Kerberos realms created, which is fine.

```
sudo krb5_newrealm
```


## 注意事项