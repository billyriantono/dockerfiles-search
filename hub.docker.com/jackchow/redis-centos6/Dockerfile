# 基于centos6基础镜像
FROM centos:6
MAINTAINER jackchow "jack_chow621@sina.com"

WORKDIR /home

#安装YUM源
RUN yum -y update && yum -y install epel-release && yum -y install redis && \
#修改绑定IP地址
    sed -i -e 's@bind 127.0.0.1@bind 0.0.0.0@g' /etc/redis.conf && \
#关闭保护模式
    sed -i -e 's@protected-mode yes@protected-mode no@g' /etc/redis.conf && \
#安装清理缓存文件
    yum clean all


# 设置环境变量
ENV TZ Asia/Shanghai

#暴露端口
EXPOSE 6379

#启动
CMD [ "/usr/bin/redis-server","/etc/redis.conf"]