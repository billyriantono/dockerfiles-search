FROM registry.cn-hangzhou.aliyuncs.com/xialintai/phpnginx
COPY / /var/www/html

#版本号
RUN echo "v@"$(date +%Y%m%d%H%M%S) >/v
RUN mkdir -p /opt/logs && chmod 0777 /opt/logs


RUN apt-get -y update && apt-get -y install  ssh \
    && mkdir /var/run/sshd && chmod 0755 /var/run/sshd \
    && sed -i 's/^PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config \
    && sed -i 's/^PasswordAuthentication.*/PermitRootLogin yes/' /etc/ssh/sshd_config \
    && sed -i 's/#PasswordAuthentication.*/PermitRootLogin yes/' /etc/ssh/sshd_config

VOLUME /root/.ssh/
CMD /usr/sbin/sshd && tail -f /etc/hosts

VOLUME /var/www/html/Business/
EXPOSE 22

#1.开启ssh服务端口
#2.生成代码运行配置脚本
#3.生成elticsearch的索引
#4.开启nginx,php服务
CMD  bash -c "/usr/sbin/sshd; phpunit ;  sh Shell/websitesuggest.sh;nginx; php-fpm"