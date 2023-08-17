# Nagios-Installation
# Steps for Install & Configure Nagios

- Create 1 ec2 instance :- t2.micro
<img width="960" alt="image" src="https://github.com/rutikdevops/Nagios-Installation/assets/109506158/8bfdb472-df8a-42aa-aafe-266c1b56c2c9">
<br></br>
```bash
ec2-user
sudo su
yum update -y
hostnamectl set-hostname Nagios
bash
```

- Install apache & php
```bash
yum install httpd php -y
```

- Install compiler
```bash
yum install gcc glibc glibc-common -y
yum install gd gd-devel -y
```

- Create User
```bash
adduser -m nagios
passwd nagios    #(enter passwd 2 times)
```

- Create Group
```bash
groupadd nagioscmd
```

```bash
usermod -aG nagioscmd nagios
usermod -aG nagioscmd apache
```

- Download Nagios
```bash
mkdir ~/downloads
cd ~/downloads
wget https://yer.dl.sourceforge.net/project/nagios/nagios-4.x/nagios-4.0.8/nagios-4.0.8.tar.gz
tar -xvzf nagios-4.0.8.tar.gz
ls
wget http://nagios-plugins.org/download/nagios-plugins-2.0.3.tar.gz
tar -xvzf nagios-plugins-2.0.3.tar.gz
ls
cd nagios-4.0.8
```

- Run Configuration script
```bash
./configure --with-command-group=nagioscmd
```

- Compile the files
```bash
make all
make install
make install-init
make install-config
make install-commandmode
```

- use this command if want to change email_id
```bash
vim /usr/local/nagios/etc/objects/contacts.cfg
```

- Congigure web interface
```bash
make install-webconf
```

- Create Nagios admin account for login
```bash
htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin    #(enter passwd 2 times)
```


- Start apache service
```bash
service httpd restart
```

- Install Nagios Plugins
```bash
cd ~/downloads
tar -xvzf nagios-plugins-2.0.3.tar.gz
cd nagios-plugins-2.0.3
```

- Configure now
```bash
./configure --with-nagios-user=nagios --with-nagios-group=nagios
```


- Compile now
```bash
make
make install
```

- Add nagios in system services
```bash
chkconfig --add nagios
chkconfig nagios on
```


- Verify now
```bash
/usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg
```



- Start services
```bash
service nagios start
service httpd restart
```

- paste public_ip with /nagios/
- username= , passwd=                ## Whatever you set


<img width="945" alt="image" src="https://github.com/rutikdevops/Nagios-Installation/assets/109506158/c586f78b-f854-4794-be83-094aa94ff6e8">












































































































