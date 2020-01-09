FROM alpine:3.7

COPY src /
RUN mysql-setup

ENTRYPOINT ["mysql-entrypoint"]

USER mysql
CMD ["mysqld", "--skip-name-resolve"]
