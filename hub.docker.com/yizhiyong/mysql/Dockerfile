FROM mysql:5.7
RUN apt-get update && apt-get install curl -y

ENTRYPOINT ["docker-entrypoint.sh"]

EXPOSE 3306
CMD ["mysqld"]
