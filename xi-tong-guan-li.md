# 高效率保证服务运行

1. Supervisor

2. Fabric/Ansible

3. Sentry收集错误信息

4. 监控系统搭建（API监控，服务器监控）

5. 集中式日志收集

6. 服务发现容器化编排


## Supervisor
```shell
1. pip install supervisor # 做service 启动程序

[unix_http_server]
file=/tmp/supervisor.sock   ; (the path to the socket file)

[inet_http_server]         ; inet (TCP) server disabled by default
port=127.0.0.1:9001        ; (ip_address:port specifier, *:port for all iface)

[rpcinterface:supervisor]
supervisor.rpcinterface_factory = supervisor.rpcinterface:make_main_rpcinterface

[supervisorctl]
serverurl=unix:///tmp/supervisor.sock ; use a unix:// URL  for a unix socket

[supervisord]
nodaemon=true
logfile=/data/log/supervisord.log
pidfile=/data/supervisord.pid

[program:XXXX]
process_name=v2-XXX-%(process_num)s
command=python server.py --port=%(process_num)s  # tornado
directory=/code
autostart = true
autorestart=true
stopasgroup=true
startsecs=2
stopsignal=HUP
stopwaitsecs=1
stdout_logfile = /data/log/stdout-%(program_name)s.log
stderr_logfile = /data/log/stderr-%(program_name)s.log
stderr_logfile_maxbytes = 20MB
numprocs=30
numprocs_start=9527


```








