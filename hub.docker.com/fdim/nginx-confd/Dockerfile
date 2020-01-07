FROM nginx:1.9

MAINTAINER Alexander Lukichev

ADD https://github.com/kelseyhightower/confd/releases/download/v0.12.0-alpha3/confd-0.12.0-alpha3-linux-amd64 /bin/confd 
RUN chmod +x /bin/confd

COPY nginx.conf /etc/nginx/nginx.conf

#proxy takes over everything
RUN rm /etc/nginx/conf.d/default.conf

COPY confd /etc/confd

COPY start.sh /start.sh
RUN chmod +x /start.sh

CMD ["/start.sh"]


