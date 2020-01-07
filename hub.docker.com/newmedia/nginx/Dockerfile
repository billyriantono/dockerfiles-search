FROM newmedia/centos
ADD nginx_signing.key /etc/pki/tls/certs/nginx_signing.key
RUN \
rpm --import /etc/pki/tls/certs/nginx_signing.key && \
rpm -ivh http://nginx.org/packages/centos/6/noarch/RPMS/nginx-release-centos-6-0.el6.ngx.noarch.rpm && \
yum install -y nginx && \
yum clean all && \
mkdir /etc/nginx/sites-enabled && \
chmod 0644 /etc/nginx/sites-enabled
ADD etc /etc
VOLUME ["/etc/nginx/sites-enabled", "/etc/nginx/conf.d", "/var/log/nginx", "/var/www"]
WORKDIR /etc/nginx
CMD ["nginx"]
EXPOSE 80
EXPOSE 443