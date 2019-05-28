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
Then install InfluxDB
```
$ sudo apt-get update && sudo apt-get install influxdb
```
Start and connect InfluxDB
```
$ sudo service influxdb start
$ influx
```
If you want to enable InfluxDB web gui, please edit the configuratio file of InfluxDB
```
sudo vi /etc/influxdb/influxdb.conf

[http]
enabled = true
bind–address = ":8083"
https–enabled = false
https–certificate = "/etc/ssl/influxdb.pem"
```
Create a new database for ONOS
```
> CREATE DATABASE onos
> use onos
> CREATE USER onos WITH PASSWORD 'onos.password' WITH ALL PRIVILEGES
```
