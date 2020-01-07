FROM mobilelive/alpine:basic
MAINTAINER mobilelive/dockerfiles

# install #

RUN apk add --update "nginx>1.10"
RUN rm -rf /var/cache/apk/*

# setup #

RUN rm -rf /app/etc ; \
      mv -f /etc/nginx /app/etc ; \
      ln -s /app/etc /etc/nginx
RUN rm -rf /app/var ; \
      mv -f /var/lib/nginx/html /app/var ; \
      ln -s /app/var /var/lib/nginx/html
RUN mv -f /var/log/nginx /app/log ; \
      ln -s /app/log /var/log/nginx
RUN mkdir /app/run ; \
      ln -s /app/run /run/nginx
RUN chown -R app:app /app

# files #

COPY default.conf /etc/nginx/nginx.conf

# cmd #

EXPOSE 443 80
CMD [ "nginx" , "-g" , "daemon off;" ]




