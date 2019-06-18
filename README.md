# ONOS_Grafana

## Prerequisites
1. InfluxDB
2. Grafana

## Installation
* InfluxDB
Update the sources
```
$ sudo apt-get update
$ sudo apt-get upgrade
```
Add and configure InfluxDB sources
```
$ curl -sL https://repos.influxdata.com/influxdb.key | sudo apt-key add -
$ source /etc/lsb-release
$ echo "deb https://repos.influxdata.com/${DISTRIB_ID,,} ${DISTRIB_CODENAME} stable" | sudo tee /etc/apt/sources.list.d/influxdb.list
```
Then install InfluxDB. Because we need to use the older version (e.g., version 0.10.3 or lower), use 'wget' to download the source and install it. Refer to [InfluxDB Client](https://launchpad.net/ubuntu/xenial/amd64/influxdb-client/0.10.0+dfsg1-1) and [InfluxDB](https://launchpad.net/ubuntu/yakkety/amd64/influxdb/0.10.0+dfsg1-1)
```
$ wget https://launchpad.net/ubuntu/xenial/amd64/influxdb-client/0.10.0+dfsg1-1
$ wget https://launchpad.net/ubuntu/yakkety/amd64/influxdb/0.10.0+dfsg1-1
$ chmod 755 influxdb*
$ sudo dpkg -i influxdb_0.10.0+dfsg1-1_amd64.deb
$ sudo dpkg -i influxdb-client_0.10.0+dfsg1-1_amd64.deb
```
Start and connect InfluxDB
```
$ sudo service influxdb start
$ influx
```
If you want to enable InfluxDB web gui (use version 0.10.3 or lower), please edit the configuratio file of InfluxDB
```
sudo vi /etc/influxdb/influxdb.conf

[admin]
enabled = true
bind-address = ":8083"
https-enabled = false
https-certificate = "/etc/ssl/influxdb.pem"
```
Create a new database for ONOS
```
> CREATE DATABASE onos
> use onos
> CREATE USER onos WITH PASSWORD 'onos.password' WITH ALL PRIVILEGES
```
Install firewalld
```
$ sudo apt install firewalld
$ sudo systemctl start firewalld
$ sudo firewall-cmd --zone=public --add-port=8086/tcp --permanent
$ sudo firewall-cmd --zone=public --add-port=8088/tcp --permanent
$ sudo firewall-cmd --zone=public --add-port=8888/tcp --permanent
$ sudo firewall-cmd --reload
$ sudo firewall-cmd --zone=public --list-port
```
## References
1. https://community.influxdata.com/t/install-specific-version-of-influxdb-in-ubuntu-16-04/4631
2. https://cloud.tencent.com/developer/article/1173608
3. http://www.andremiller.net/content/grafana-and-influxdb-quickstart-on-ubuntu
4. https://www.digitalocean.com/community/tutorials/how-to-install-prometheus-on-ubuntu-16-04 (good)
5. https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-grafana-on-ubuntu-16-04 (good)
