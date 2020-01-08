# nodejs

FROM centos:centos6

# install EPEL
RUN rpm -Uvh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm \
 && yum update -y \
 && yum upgrade

# install node & npm & git
RUN yum install -y npm git

CMD ["node"]