FROM openshift/base-centos7
MAINTAINER hookbrother <hookbrother@gmail.com>

# 安装软件
RUN rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm && \
  yum install -y nginx && \
  yum clean all && \
  rm -rf var/cache/yum

# 创建网站项目文件夹
RUN mkdir /usr/www && \
  chown nginx:nginx -R /usr/www && \
  chmod a+w -R /usr/www

# 设置时区
RUN /bin/cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
&& echo 'Asia/Shanghai' >/etc/timezone \

COPY nginx.conf /etc/nginx/nginx.conf
COPY run.sh /run.sh
RUN chmod 755 /*.sh

VOLUME ["/usr/www"]

EXPOSE 80 443

ENTRYPOINT ["/run.sh"]