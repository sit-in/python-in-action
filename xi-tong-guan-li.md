# 高效率保证服务运行

1. Supervisor

2. Fabric/Ansible/Salt stack

3. Sentry收集错误信息

4. 监控系统搭建（API监控，服务器监控）

5. 集中式日志收集

6. 服务发现容器化编排


## Supervisor

[使用 supervisor 管理进程 - 李林克斯](http://liyangliang.me/posts/2015/06/using-supervisor/)

## Fabric/Ansible/Salt

[运维管理工具的对比Puppet、Chef、Ansible和SaltStack、Fabric - CSDN博客](https://blog.csdn.net/zzq900503/article/details/80143740)

1. Fabric发布版本，自动化精简输入指令 类似Makefile(shell 能做 Python）
2. 机器多，需要控制建议使用 ansible 发布版本初始化服务器，成本比Fabric高一些

## Sentry

[使用docker-compose运行错误收集工具Sentry | Pegasus' Blog](http://ningning.today/2016/10/18/python/docker-sentry/)


