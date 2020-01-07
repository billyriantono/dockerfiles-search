FROM golang:1.8

VOLUME /var/app

COPY entrypoint.sh /entrypoint.sh
RUN ["chmod", "+x", "/entrypoint.sh"]

EXPOSE 9000

ENTRYPOINT ["/entrypoint.sh"]