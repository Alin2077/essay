## Redis使用lua脚本
* Redis通过EVAL命令执行lua脚本，保证原子性
## Redis使用示例
* eval "redis.call('set','k1','v1') redis.call('expire','k1','30') return redis.call('get','k1')"
* eval "redis.call('mset',KEYS[1],ARGV[1],KEYS[2],ARGV[2])" 2 k1 k2 v1 v2   