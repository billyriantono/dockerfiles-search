# 基于我自己的ubuntu-sshd 镜像
FROM caseycui/ubuntu-sshd

# 维护者
LABEL maintainer="CaseyCui cuikaidong@foxmail.com"

# 1. 安装(推荐项中有ssl-certs，需要一并安装)
# 2. 创建 /var/lock/apache2 目录（启动需要）
RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -yq  \
        apache2 \
    && rm -rf /var/lib/apt/lists/* \
    && mkdir -p /var/lock/apache2

# 添加脚本，并设置权限(创建该脚本时就增加执行权限)
COPY run-apache2.sh /run-apache2.sh

# 添加挂载点 /var/www
VOLUME /var/www

# 设置 apache 相关变量，在容器启动的时候可以使用 -e 参数替换
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_SERVERADMIN admin@localhost
ENV APACHE_SERVERNAME localhost
ENV APACHE_SERVERALIAS docker.localhost
ENV APACHE_DOCUMENTROOT /var/www

# 暴露 80 端口
EXPOSE 80

# 工作目录
WORKDIR /var/www

# 启动命令
CMD ["/run-apache2.sh"]
