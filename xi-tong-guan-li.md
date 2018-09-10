# 高效率保证服务运行

1. Supervisor

2. Fabric/Ansible

3. Sentry收集错误信息

4. 监控系统搭建（API监控，服务器监控）

5. 集中式日志收集

6. 服务发现容器化编排


## Supervisor
```shell
1. pip install supervisor # 可以通过sh做service 启动程序，避免启动失效

# supervisord.conf

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
directory=/code  # 这儿在docker容器目录
autostart = true
autorestart=true
stopasgroup=true
startsecs=2
stopsignal=HUP
stopwaitsecs=1
stdout_logfile = /data/log/stdout-%(program_name)s.log
stderr_logfile = /data/log/stderr-%(program_name)s.log
stderr_logfile_maxbytes = 20MB
numprocs=10 # 启动多少个
numprocs_start=9527

```
[使用 supervisor 管理进程 - 李林克斯](http://liyangliang.me/posts/2015/06/using-supervisor/)

## Fabric/Ansible/Salt

[运维管理工具的对比Puppet、Chef、Ansible和SaltStack、Fabric - CSDN博客](https://blog.csdn.net/zzq900503/article/details/80143740)

1. Fabric发布版本，自动化精简输入指令 类似Makefile(shell 能做 Python）
2. 机器多，需要控制建议使用 ansible 发布版本初始化服务器，成本比Fabric高一些

## Sentry

[使用docker-compose运行错误收集工具Sentry | Pegasus' Blog](http://ningning.today/2016/10/18/python/docker-sentry/)


