FROM ubuntu:precise
MAINTAINER Music Glue <devteam@musicglue.com>

RUN apt-get update -qq
RUN bash -c "export DEBIAN_FRONTEND=noninteractive; apt-get -q -y install mysql-server-5.5"

ADD ./scripts/ /scripts
ADD ./config/my.cnf /etc/mysql/conf.d/my.cnf

EXPOSE 3306
ENTRYPOINT ["/scripts/mysql"]