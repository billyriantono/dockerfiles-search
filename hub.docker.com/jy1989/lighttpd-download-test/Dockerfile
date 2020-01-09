# Dockerfile for lighttpd-download-test

FROM alpine
MAINTAINER jy
RUN apk add --update --no-cache \
	lighttpd \
	lighttpd-mod_auth \
  && rm -rf /var/cache/apk/* \
  && dd if=/dev/zero of=/var/www/localhost/htdocs/100M.zip bs=1M count=100

## workaround for bug preventing sync between VirtualBox and host
# http://serverfault.com/questions/240038/lighttpd-broken-when-serving-from-virtualbox-shared-folder
RUN echo server.network-backend = \"writev\" >> /etc/lighttpd/lighttpd.conf

COPY etc/lighttpd/* /etc/lighttpd/
COPY /var/www/localhost/htdocs/* /var/www/localhost/htdocs

EXPOSE 80

VOLUME /var/www/localhost
VOLUME /etc/lighttpd

CMD ["lighttpd", "-D", "-f", "/etc/lighttpd/lighttpd.conf"]
