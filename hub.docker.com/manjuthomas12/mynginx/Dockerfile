FROM nginx
RUN apt-get update &&  apt-get install nginx -y 
RUN rm -rf /var/www/html/*
COPY index.html /var/www/html/
CMD nginx -g  ‘daemon off;’
EXPOSE 8080 80
