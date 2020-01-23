FROM nginx:alpine
COPY default.conf /etc/nginx/conf.d/default.conf
COPY 10-www /etc/init.d/
RUN chmod a+x /etc/init.d/10-www

ENV WEBPAGECONTENT="Edit WEBPAGECONTENT environment variable to fit your needs"
RUN echo $WEBPAGECONTENT > /usr/share/nginx/html/index.html
