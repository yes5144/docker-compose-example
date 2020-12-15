## prometheus

### grafana
```ini
## 常用模板编号: 
node-exporter: cn/8919,en/11074
k8s: 13105
docker: 12831
alertmanager: 9578
blackbox_exporter: 9965
```
### 结构
```ini
.
├── config
│   ├── alertmanager
│   │   ├── alertmanager.yml
│   │   └── templates
│   │       ├── test.tmpl
│   │       ├── wechat.default.message
│   │       └── wechat.tmpl
│   ├── cadvisor
│   ├── grafana
│   ├── node-exporter
│   └── prometheus
│       ├── prometheus.yml
│       └── rules
│           ├── docker-monitor.yml
│           ├── host-base-monitor.yml
│           ├── hoststats-alert.yml
│           └── node.yml.simple
├── docker-compose.yml
└── readme.md
```

8 directories, 11 files
### images and version
```ini
[root@yes5144 docker-compose4prometheus-alertmanager-grafana]# docker-compose --version
docker-compose version 1.18.0, build 8dd22a9
[root@yes5144 docker-compose4prometheus-alertmanager-grafana]# docker --version
Docker version 18.06.1-ce, build e68fc7a


[root@yes5144 ~]# docker images |grep prom
prom/prometheus                                 latest              6fa696e177e3        4 weeks ago         168MB
prom/alertmanager                               latest              c876f5897d7b        6 months ago        55.5MB
prom/node-exporter                              latest              0e0218889c33        6 months ago        26.4MB
prom/mysqld-exporter                            latest              432cdd0a0e7c        16 months ago       17.5MB
grafana/grafana                                 latest              1eaf753fbbdd        4 weeks ago         186MB
centos/mysql-57-centos7                         latest              f83a2938370c        14 months ago       452MB


[root@yes5144 docker-compose4prometheus-alertmanager-grafana]# docker ps
CONTAINER ID        IMAGE                         COMMAND                  CREATED             STATUS              PORTS                    NAMES
7fb9aa144852        prom/prometheus:latest        "/bin/prometheus --c…"   3 hours ago         Up 3 hours                                   prometheus
4b4e814d6062        grafana/grafana:latest        "/run.sh"                3 hours ago         Up 3 hours                                   grafana
3d3560c70cb2        prom/mysqld-exporter:latest   "/bin/mysqld_exporter"   3 hours ago         Up 21 minutes                                mysqld-exporter
c333dd303416        google/cadvisor:latest        "/usr/bin/cadvisor -…"   3 hours ago         Up 3 hours                                   cadvisor
e273bbe86f2d        prom/node-exporter:latest     "/bin/node_exporter …"   3 hours ago         Up 3 hours                                   node-exporter
cd9260534336        prom/alertmanager:latest      "/bin/alertmanager -…"   3 hours ago         Up 3 hours                                   alertmanager
1dc31cd66c10        centos/mysql-57-centos7       "container-entrypoin…"   3 hours ago         Up 3 hours          0.0.0.0:3306->3306/tcp   cranky_agnesi


[root@yes5144 docker-compose4prometheus-alertmanager-grafana]# docker exec 7fb9aa144852 /bin/prometheus --version
prometheus, version 2.22.2 (branch: HEAD, revision: de1c1243f4dd66fbac3e8213e9a7bd8dbc9f38b2)
  build user:       root@f7d7e91063f0
  build date:       20201116-12:43:43
  go version:       go1.15.5
  platform:         linux/amd64
[root@yes5144 docker-compose4prometheus-alertmanager-grafana]# docker exec 3d3560c70cb2 /bin/mysqld_exporter --version
mysqld_exporter, version 0.12.1 (branch: HEAD, revision: 48667bf7c3b438b5e93b259f3d17b70a7c9aff96)
  build user:       root@0b3e56a7bc0a
  build date:       20190729-12:35:58
  go version:       go1.12.7
[root@yes5144 docker-compose4prometheus-alertmanager-grafana]# docker exec c333dd303416 /usr/bin/cadvisor --version
cAdvisor version v0.32.0 (8949c822)
[root@yes5144 docker-compose4prometheus-alertmanager-grafana]# docker exec e273bbe86f2d /bin/node_exporter --version
node_exporter, version 1.0.1 (branch: HEAD, revision: 3715be6ae899f2a9b9dbfd9c39f3e09a7bd4559f)
  build user:       root@1f76dbbcfa55
  build date:       20200616-12:44:12
  go version:       go1.14.4
[root@yes5144 docker-compose4prometheus-alertmanager-grafana]# docker exec cd9260534336 /bin/alertmanager --version
alertmanager, version 0.21.0 (branch: HEAD, revision: 4c6c03ebfe21009c546e4d1e9b92c371d67c021d)
  build user:       root@dee35927357f
  build date:       20200617-08:54:02
  go version:       go1.14.4
[root@yes5144 docker-compose4prometheus-alertmanager-grafana]# docker exec  4b4e814d6062 /usr/share/grafana/bin/grafana-cli --version
Grafana CLI version 7.3.3

```
### docker mysql
docker run -d -p 3306:3306  -e  MYSQL_ROOT_PASSWORD=123456  centos/mysql-57-centos7
