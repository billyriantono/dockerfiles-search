FROM centos:latest

MAINTAINER akibe <dev@akibe.com>

# make sure the package repository is up to date
# http://nginx.org/en/linux_packages.html#stable
RUN rpm -ivh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
RUN yum -y install nginx
RUN yum clean all

EXPOSE 80

ENTRYPOINT ["/usr/sbin/nginx", "-g", "daemon off;"]
