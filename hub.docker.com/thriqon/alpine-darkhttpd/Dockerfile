FROM alpine:3.4
RUN apk add --no-cache darkhttpd && mkdir -p /www

VOLUME /www
CMD ["darkhttpd", "/www"]
EXPOSE 80
