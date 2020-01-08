FROM redis:5

ADD docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh

EXPOSE 26379

ENTRYPOINT [ "/docker-entrypoint.sh" ]
