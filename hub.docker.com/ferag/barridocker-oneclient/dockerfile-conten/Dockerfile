#Choose apache alpine
FROM alpine

RUN apk no-cache update

RUN apk add --no-cache ca-certificates openssl openssl-dev \
pcre-dev apache2 apache2-proxy apache2-ssl

RUN rm -R /etc/apache2/*
ADD configs/apache2 /etc/apache2

#Ports
EXPOSE 80 443

#Volumes
VOLUME /opt/proxy-conf
VOLUME /opt/ssl

#Launch Apache2 on FOREGROUND
COPY apache-proxy-start.sh /opt/
RUN chmod +x /opt/apache-proxy-start.sh
ENTRYPOINT ["/opt/apache-proxy-start.sh"]
