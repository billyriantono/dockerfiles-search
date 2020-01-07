FROM miyamotota/centos67-base:latest

MAINTAINER miyamoto_ta <miyamoto_ta@zoho.com>

RUN rpm -ivh http://nginx.org/packages/centos/6/noarch/RPMS/nginx-release-centos-6-0.el6.ngx.noarch.rpm
RUN yum -y install nginx && yum clean all

COPY ./etc/nginx/nginx.conf /etc/nginx/
COPY ./etc/nginx/conf.d/default.conf /etc/nginx/conf.d/

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
