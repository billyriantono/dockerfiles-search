FROM centos:7
MAINTAINER Alex Drahon <adrahon@gmail.com>
RUN yum install -y https://repos.fedorapeople.org/repos/openstack/openstack-kilo/rdo-release-kilo-1.noarch.rpm &&\
    yum install -y \
      mariadb-galera-server \
      rsync \
      socat &&\
    yum clean all
COPY galera.cnf /etc/my.cnf.d/galera.cnf
COPY ./start /
EXPOSE 3306 4444 4567 4568
CMD ["/start"]
