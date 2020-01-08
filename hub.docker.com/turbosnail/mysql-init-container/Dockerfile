FROM alpine:3.9
RUN apk add mysql-client
RUN rm -rfv /var/lib/apk/cache
COPY entrypoint.sh /usr/bin/entypoint
RUN chmod +x /usr/bin/entypoint

ENV MYSQL_PORT=3306
ENV MYSQL_ROOT_USERNAME=root
WORKDIR /root
ENTRYPOINT ["/usr/bin/entypoint"]