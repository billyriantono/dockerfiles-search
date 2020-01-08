# download centos 7
FROM centos:7

# make update of the system without cache
RUN yum -y update && \
    yum -y upgrade && \
    yum clean all && \
    rm -rf /var/cache/yum 
