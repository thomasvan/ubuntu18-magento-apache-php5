### Run the latest magento 2 on Ubuntu 18.04.1 LTS, including: 
- Shell In A Box – A Web-Based SSH Terminal - version 2.x
- Apache 2.4.x
- php-fpm 5.6.x
- elasticsearch 2.4.6
- redis server version 4.x
- mysql version 5.7.x
- phpMyAdmin latest version
- composer latest version
- You can also handle all services using supervisord 3. <container_ip>:9011 or commandline: 

```bash
magento@c9786d14b245:~/files/html$ sudo supervisorctl 
Apache2                          RUNNING   pid 835, uptime 3:02:33
BroswerBased-SSH                 RUNNING   pid 18, uptime 3:15:58
Cron                             RUNNING   pid 19, uptime 3:15:58
ElasticSearch_2.x_9200           STOPPED   Not started
MySQL                            RUNNING   pid 14, uptime 3:15:58
PHP-FPM                          RUNNING   pid 13, uptime 3:15:58
RedisServer                      STOPPED   Not started
System-Log                       RUNNING   pid 21, uptime 3:15:58

```
___

### Usage
Services and ports exposed
- Shell In A Box – A Web-Based SSH Terminal - http://<contaner_ip>:4200
- ElasticSearch 2.4.6 - <contaner_ip>:9000
- MySQL - <contaner_ip>:3306
- phpMyAdmin http://<contaner_ip>/phpmyadmin
- Nginx and php-fpm 5.6.x - http://<contaner_ip> and https://<contaner_ip> for web browsing
- Redis - <contaner_ip>:6379

#### Sample container initialization: 

```bash
$ docker run -v <your-webapp-root-directory>:/home/magento/files/html -p 4222:4200 -p 9022:9011 --name docker-name -d thomasvan/ubuntu18-magento-apache-php5-elasticsearch-mysql-phpmyadmin-redis-composer:latest
```
___

After starting the container ubuntu18-magento-apache-php5-elasticsearch-mysql-phpmyadmin-redis-composer, please check to see if it has started and the port mapping is correct. This will also report the port mapping between the docker container and the host machine.

##### Accessing containers by port mapping
```bash
$ docker ps

0.0.0.0:9011->9022/tcp, 0.0.0.0:4022->4200/tcp
```
___


You can then visit the following URL in a browser on your host machine to get started(account: magento/magento): `http://125.6.0.1:2222`

You can start/stop/restart and view the error logs of nginx and php-fpm services: `http://125.6.0.1:9011`

##### Accessing containers by internal IP

_For Windows 10, you need to [add route: route add 172.15.6.0 MASK 255.255.0.0 10.0.75.2](https://forums.docker.com/t/connecting-to-containers-ip-address/18817/13) manually before using one of the ways below to get internal IP:_
- Looking into the output of `docker logs <container-id>`:
- Using [docker inspect](https://docs.docker.com/engine/reference/commandline/inspect/parent-command) command
- Checking the ~/readme.txt file by using [Web-Based SSH Terminal](http://125.6.0.1:2222)
___
 

```bash
c9786d14b245 login: magento
Password:
Welcome to Ubuntu 18.04.1 LTS ...

magento@c9786d14b245:~$ cat ~/readme.txt
IP Address : 172.15.6.2
Web Directory : /home/magento/files/html
SSH/SFTP User : magento/magento
ROOT User : root/root
Database Host : localhost
Database Name : magento
Database User : magento/magento
DB ROOT User : root/root 
phpMyAdmin : https://172.15.6.2/phpmyadmin
```
___

_Now as you've got all that information, you can set up magento and access the website via IP Address or creating an [alias in hosts](https://support.rackspace.com/how-to/modify-your-hosts-file/) file_

```bash
c9786d14b245 login: magento
Password:
Welcome to Ubuntu 18.04.1 LTS ...

magento@c9786d14b245:~$ cd files/html/
magento@c9786d14b245:~/files/html$ echo "install magento 2 here..."
install magento 2 here...
magento@c9786d14b245:~/files/html$ echo "all set, you can browse your website now"
all set, you can browse your website now
magento@c9786d14b245:~/files/html$ 
   ```
___


_If anyone has suggestions please leave a comment on [this GitHub issue](https://github.com/thomasvan/ubuntu18-magento-apache-php5/issues/2)._

_Requests? Just make a comment on [this GitHub issue](https://github.com/thomasvan/ubuntu18-magento-apache-php5/issues/1) if there's anything you'd like added or changed._
