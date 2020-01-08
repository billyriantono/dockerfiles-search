FROM ubuntu:12.04
MAINTAINER Denmark Garcia
# This is just a sample git and docker

ADD ./mysql-setup.sh /tmp/mysql-setup.sh
RUN /bin/sh /tmp/mysql-setup.sh

# Adding this will expose mysql on a random host port. It's recommended to avoid this. Other containers on the same
# host can use the service without it.
#EXPOSE 3306

CMD ["/usr/sbin/mysqld"]
