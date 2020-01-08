FROM mysql:5.7.9

RUN apt-get update && apt-get install -y perl --no-install-recommends


VOLUME /var/lib/mysql

COPY my.cnf.tmpl /tmp/my.cnf.tmpl
# need random.sh because otherwise, ENV $RANDOM is not set
COPY random.sh /tmp/random.sh
RUN /tmp/random.sh

COPY docker-entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

EXPOSE 3306
CMD ["mysqld"]
