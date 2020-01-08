FROM ubuntu:14.04

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get -y upgrade

RUN apt-get install -y mysql-server nano
ADD my.cnf /etc/mysql/conf.d/my.cnf 
ADD init.sh /usr/local/bin/init.sh
RUN chmod +x /usr/local/bin/init.sh

VOLUME ["/var/lib/mysql"]
CMD ["/usr/local/bin/init.sh"]
EXPOSE 3306
