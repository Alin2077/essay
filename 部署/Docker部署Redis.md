### 1.准备工作
* 下载docker以及redis镜像
### 2.配置文件
```yml
# 远程连接
bind 0.0.0.0 ::0
protected-mode no
# 端口
port 6379
# 超时时间
timeout 0
# 最大连接数
maxclients 10
# 是否以守护进程方式运行，docker启动可设置为no
daemonize no
# 密码
requirepass "irony"

# RDB相关
# 配置保存规则 例如：9000秒内有100次key变动就触发一次bgsave
save 9000 100
# 当RDB无法写入磁盘时，停止接收写命令，默认为yes
stop-writes-on-bgsave-error yes
# 是否采用LZF算法进行压缩，默认为yes
rdbcompression yes
# 使用CRC64算法来进行数据校验，默认为yes
rdbchecksum yes
# 存储快照的文件名，默认为dump.rdb
dbfilename dump_1.rdb
# 指定数据库和AOF文件存放的位置，默认为当前目录
dir /data

# AOF
# 是否开启AOF，默认为no
appendonly yes
# AOF文件名，默认为appendonly.aof
appendfilename appendonly_1.aof
# 同步AOF文件的策略 always(每个写命令都同步)、everysec(每秒同步一次,默认)、no(不主动同步)
appendfsync everysec
# 在重写AOF文件时，是否禁用fsync，默认为no，不建议开启
no-appendfsync-on-rewrite no
# 是否自动触发AOF重写
# 达到上次重写多少百分比触发重写
auto-aof-rewrite-percentage 95
# 文件达到多大触发重写
auto-aof-rewrite-min-size 64
```
* 注意：配置文件中配置目录都是针对镜像内的目录，不是当前conf文件的目录，使用绝对路径
### 3.启动
> docker run -p 6379:6379 --name redis -v /usr/local/myData/redisData:/data \
    -v /usr/local/myConfig/redis.conf:/etc/redis/redis.conf 
    -d redis redis-server /etc/redis/redis.conf
* 上面的命令中，将第2步配置好的conf文件映射至镜像内，存放文件目录/redisData也映射到镜像内，-d redis 是以守护进程启动，redis-server /etc/redis/redis.conf 则是运行的命令
### 4.验证
> docker ps
> docker ps -a
> docker exec -it <CONTAINER ID> redis-cli