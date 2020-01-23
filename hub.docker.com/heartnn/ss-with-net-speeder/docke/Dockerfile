FROM alpine:3.8

LABEL maintainer "Ben Roberts <ben@headsnet.com>"

RUN apk --no-cache add nginx

RUN mkdir /run/nginx

COPY nginx.conf /etc/nginx/nginx.conf
RUN rm /etc/nginx/conf.d/default.conf

EXPOSE 80

COPY scripts/entrypoint.sh /
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
