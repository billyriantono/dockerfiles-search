FROM mysql:5.7 as upstream

FROM scratch
COPY --from=upstream / /

ENV GOSU_VERSION 1.7
ENV MYSQL_MAJOR 5.7
ENV MYSQL_VERSION 5.7.25-1debian9

VOLUME /var/lib/mysql

ENTRYPOINT ["docker-entrypoint.sh"]

# only expose port 3306, but not 33060,
# as the upstream Dockerfile does
EXPOSE 3306

CMD ["mysqld"]
