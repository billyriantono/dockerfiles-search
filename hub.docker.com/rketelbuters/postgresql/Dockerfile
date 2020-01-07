FROM centos:7
MAINTAINER Robin Ketelbuters <robinketelbuters@gmail.com>
ENV container docker
ENV PGDATA /var/lib/pgsql/data
RUN yum update -y \
&&  yum install -y postgresql postgresql-server \
&&  yum clean all \
&&  systemctl enable postgresql.service
EXPOSE 5432
VOLUME /var/lib/pgsql/data
ADD initdb.sh /
STOPSIGNAL SIGRTMIN+3
CMD [ "/sbin/init" ]
