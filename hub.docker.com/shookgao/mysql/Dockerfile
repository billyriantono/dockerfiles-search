FROM mysql:5
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo "Asia/Shanghai" > /etc/timezone
RUN confile=/etc/mysql/conf.d/docker.cnf && echo "character_set_server=utf8" >> $confile && \
    echo "server-id=1" >> $confile && echo "log_bin" >> $confile && echo "slow_query_log" >> $confile
