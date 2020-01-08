FROM centos:7

MAINTAINER Pedro Mauricio Echeverry Rey <pedromauricioecheverry@gmail.com>

RUN echo -e "[mongodb]\nname=MongoDB Repository\nbaseurl=http://downloads-distro.mongodb.org/repo/redhat/os/`uname -m`/\ngpgcheck=0\nenabled=1" > /etc/yum.repos.d/mongodb.repo

RUN yum -y update && yum -y install mongodb-org-server mongodb-org-shell mongodb-org-tools && \
    yum clean all && \
    mkdir -p /var/lib/mongo && \
    chown -R mongod:mongod /var/lib/mongo

VOLUME ["/var/lib/mongo"]

EXPOSE 27017

CMD ["/usr/bin/mongod", "--dbpath", "/var/lib/mongo"]
