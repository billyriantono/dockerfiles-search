FROM alpine:3.2

#RUN mkdir -p /var/www/site

ADD www /var/www/site

RUN rm -rf  /var/www/site/application/cache
RUN rm -rf  /var/www/site/application/logs

RUN mkdir  /var/www/site/application/cache
RUN mkdir  /var/www/site/application/logs

RUN chmod -R 777 /var/www/site/application/cache
RUN chmod -R 777 /var/www/site/application/logs

VOLUME ["/var/www/site"]
CMD ["true"]