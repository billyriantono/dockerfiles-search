FROM gliderlabs/alpine:3.1
RUN apk-install nginx bash perl openssl

RUN rm -v /etc/nginx/nginx.conf && \
        rm -v /etc/init.d/nginx && \
        mkdir -p /tmp/nginx && \
        mkdir /etc/nginx/ssl

RUN openssl req \
        -new \
        -newkey rsa:4096 \
        -days 365 \
        -nodes \
        -x509 \
        -subj "/C=CA/ST=British Columbia/L=Vancouver/O=Beanworks Solutions Inc./OU=Engineering/CN=beanworksapi" \
        -keyout /etc/nginx/ssl/beanworksapi.key \
        -out /etc/nginx/ssl/beanworksapi.crt

RUN echo "daemon off;" >> /etc/nginx/nginx.conf

EXPOSE 8443
EXPOSE 8888
EXPOSE 8080

COPY nginx.bean.conf /etc/nginx/
COPY entrypoint.sh /

CMD ["/entrypoint.sh"]
