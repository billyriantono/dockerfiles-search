FROM alpine:latest
MAINTAINER MsWebmaster

WORKDIR /app

COPY ./startup.sh /

RUN chmod +x /startup.sh \
&& apk --update add mysql mysql-client bash \
&& rm -rf /var/cache/apk/*

VOLUME /app /etc/mysql/conf.d

COPY my.cnf /etc/mysql/my.cnf

EXPOSE 3306

ENTRYPOINT [ "/startup.sh" ]
CMD [ "mysqld", "--user=root" ]
