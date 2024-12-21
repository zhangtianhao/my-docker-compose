[docker compose 最佳实践之 prometheus-grafana](https://github.com/docker/awesome-compose/tree/master/prometheus-grafana)  



```
.
├── README.md
├── compose.yaml
├── grafana
│   └── datasource.yml
├── prometheus
│   └── prometheus.yml
└── telegraf
    └── telegraf.conf

4 directories, 5 files
```

# 使用 docker compose 进行部署
```bash
docker compose up -d
```

# 预期结果
列出三个正在运行的容器
```bash
NAME         IMAGE                    COMMAND                  SERVICE      CREATED             STATUS         PORTS
grafana      grafana/grafana:11.4.0   "/run.sh"                grafana      About an hour ago   Up 9 seconds   0.0.0.0:3000->3000/tcp
prometheus   prom/prometheus:v3.0.1   "/bin/prometheus --c…"   prometheus   About an hour ago   Up 9 seconds   0.0.0.0:9090->9090/tcp
telegraf     telegraf:1.33.0          "/entrypoint.sh tele…"   telegraf     About an hour ago   Up 9 seconds   0.0.0.0:8092->8092/udp, 0.0.0.0:8094->8094/tcp, 0.0.0.0:8125->8125/udp, 0.0.0.0:9273->9273/tcp
```
访问 telegraf 提供指标数据的 /metrics 端点
```bash
curl localhost:9273/metrics
```
访问 prometheus 程序本身提供指标数据的 /metrics 端点
```bash
curl localhost:9090/metrics
```
访问 grafana 提供指标数据的 /metrics 端点
```
curl localhost:3000/metrics
```

打开 http://localhost:3000 访问 grafana 主页面，并使用 docker compose 中配置的用于名和密码（`admin` 和 `grafana`）进行登录。