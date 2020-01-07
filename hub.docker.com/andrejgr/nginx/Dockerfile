FROM nginx:1.8
#ADD nginx.conf /etc/nginx/
RUN rm /etc/nginx/conf.d/default.conf
ADD default.conf /etc/nginx/conf.d/
RUN usermod -u 1000 www-data
EXPOSE 80
EXPOSE 443
