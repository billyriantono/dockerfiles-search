FROM yakeworld/nginx-alpine
MAINTAINER yakeworld@gmail.com 
RUN apk add --no-cache --virtual .build-deps openssl \
    && mkdir -p /etc/nginx/external \
    && wget --no-check-certificate https://raw.githubusercontent.com/yakeworld/nginx-alpine-ssl/master/basic.conf -O /etc/nginx/conf.d/basic.conf \
  	&& wget --no-check-certificate https://raw.githubusercontent.com/yakeworld/nginx-alpine-ssl/master/ssl.conf -O /etc/nginx/conf.d/ssl.conf \
    && wget --no-check-certificate https://raw.githubusercontent.com/yakeworld/nginx-alpine-ssl/master/nginx.conf -O /etc/nginx/nginx.conf \
    && wget --no-check-certificate https://raw.githubusercontent.com/yakeworld/nginx-alpine-ssl/master/entrypoint.sh -O /opt/entrypoint.sh \
    && chmod a+x /opt/entrypoint.sh
ENTRYPOINT ["/opt/entrypoint.sh"]

CMD ["nginx"] 
