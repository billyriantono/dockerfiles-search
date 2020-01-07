FROM mobilelive/alpine:basic
MAINTAINER mobilelive/dockerfiles

# install #

RUN apk add --update \
      "apache2>2.4" \
      apache2-error \
      apache2-icons \
      apache2-ldap \
      apache2-proxy \
      apache2-proxy-html \
      apache2-ssl \
      apache2-utils \
      apache2-webdav \
      ;
RUN ln -s /usr/lib/libxml2.so.2 /usr/lib/libxml2.so
RUN rm -rf /var/cache/apk/*

# setup #

RUN rm -rf /app/etc ; \
      mv -f /etc/apache2 /app/etc ; \
      ln -s /app/etc /etc/apache2
RUN rm -rf /app/var ; \
      mv -f /var/www/localhost /app/var ; \
      ln -s /app/var /var/www/localhost
RUN mv -f /var/log/apache2 /app/log ; \
      ln -s /app/log /var/log/apache2
RUN mkdir /app/run ; \
      ln -s /app/run /run/apache2
RUN chown -R app:app /app

# files #

COPY default.conf /etc/apache2/httpd.conf

# cmd #

EXPOSE 443 80
CMD [ "httpd" , "-D" , "FOREGROUND" ]




