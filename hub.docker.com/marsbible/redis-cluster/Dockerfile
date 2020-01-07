FROM grokzen/redis-cluster:5.0.5

MAINTAINER kevin ma <redshift@outlook.com>

RUN sh -c "echo requirepass \"redisdev\" >> /redis-conf/redis-cluster.tmpl" && \
 sh -c "echo requirepass \"redisdev\" >> /redis-conf/redis.tmpl" && \
 sh -c "echo masterauth \"redisdev\" >> /redis-conf/redis-cluster.tmpl" && \
 sh -c "sed -i 's/src\/redis-cli --cluster/src\/redis-cli -a redisdev --cluster/' /docker-entrypoint.sh"
