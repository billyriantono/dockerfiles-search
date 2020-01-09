FROM inviqa/base
MAINTAINER Mike Simons <msimons@inviqa.com>

RUN rpm -Uhv http://www.percona.com/downloads/percona-release/redhat/0.1-3/percona-release-0.1-3.noarch.rpm
RUN yum install -y Percona-Server-server-56 Percona-Server-client-56 && yum clean all

ADD files/ /
