FROM mysql
MAINTAINER Paul Liljenberg "liljenberg.paul@gmail.com"

ADD docker-entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

EXPOSE 3306
CMD ["mysqld", "--datadir=/var/lib/mysql", "--user=mysql"]

