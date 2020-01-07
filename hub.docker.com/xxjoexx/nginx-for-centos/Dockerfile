FROM centos:7

# nginxリポジトリ追加
# nginxインストール
RUN yum -y update && \
  rpm -ivh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm && \
  yum install nginx -y 

ADD nginx.conf /etc/nginx/nginx.conf
ADD fastcgi.conf /etc/nginx/fastcgi.conf
ADD server.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["/usr/sbin/nginx", "-g", "daemon off;"]
