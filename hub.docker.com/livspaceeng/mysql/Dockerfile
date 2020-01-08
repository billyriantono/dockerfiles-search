FROM mysql:5.6.41

RUN apt-get update && apt-get install -y s3cmd

COPY docker-entrypoint.sh /usr/local/bin/

RUN chmod +x  /usr/local/bin/docker-entrypoint.sh

ENTRYPOINT ["docker-entrypoint.sh"]

EXPOSE 3306
CMD ["mysqld"]
