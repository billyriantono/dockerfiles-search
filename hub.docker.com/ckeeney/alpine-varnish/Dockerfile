FROM alpine:latest
MAINTAINER CJ Keeney <cliffordkeeney@gmail.com>
RUN apk update && apk upgrade && apk add varnish
VOLUME /etc/varnish/
EXPOSE 80
ENTRYPOINT ["varnishd"]
CMD ["-f", "/etc/varnish/default.vcl", "-F"]