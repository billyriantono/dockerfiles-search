
FROM daocloud.io/centos:7

LABEL maintainer docker_user<docker_user@email.com>

ADD nginx.repo /etc/yum.repos.d/

RUN yum update -y && yum install -y wget \
&& wget -O /etc/yum.repos.d/CentOs-Base.repo http://mirrors.163.com/.help/CentOS7-Base-163.repo \
&& yum makecache \
&& yum update -y \
&& yum install -y vim \
&& yum install -y nginx \
&& yum install -y net-tools \
&& echo "daemon off;" >> /etc/nginx/nginx.conf \
&& echo "master_process off;" >> /etc/nginx/nginx.conf
# Define mountable directories.
VOLUME ["/usr/share/nginx", "/etc/nginx/conf.d", "/var/log/nginx"]
# Define working directory.
WORKDIR /etc/nginx
# Define default command.
CMD ["/usr/sbin/nginx"]
# Expose ports.
EXPOSE 80
EXPOSE 443
