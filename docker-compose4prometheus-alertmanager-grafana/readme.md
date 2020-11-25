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
