FROM logstash:5
#安装input插件
RUN logstash-plugin install logstash-input-jdbc
#安装output插件
RUN logstash-plugin install logstash-output-elasticsearch
#容器启动时执行的命令.(CMD 能够被 docker run 后面跟的命令行参数替换)
CMD ["-f", "/some/config-dir/logstash-mysql-es.conf"]
