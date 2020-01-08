FROM centos

MAINTAINER Michal Wasilewski mwasilewski@gmx.com


# copy nginx repo
# epel repo has old version of nginx & much more dependencies
# if both are present it will be installed from nginx repo because of
# version comparison by yum
COPY nginx.repo /etc/yum.repos.d/

# install nginx
RUN yum -y install nginx \
    && yum clean all
