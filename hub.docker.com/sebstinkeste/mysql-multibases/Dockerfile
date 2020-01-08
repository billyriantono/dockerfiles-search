FROM mysql:5.5

ENV LOCALTIME Europe/Paris

COPY docker-entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

CMD ["mysqld"]

