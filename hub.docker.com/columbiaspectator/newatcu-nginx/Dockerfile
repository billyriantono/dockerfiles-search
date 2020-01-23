# This file is only meant to be used with the generated static files inside build folder
# Please run `cp Dockerfile.static build/Dockerfile` if you are doing it manually
FROM nginx:1.10
ADD . /var/www/static-site
RUN rm /etc/nginx/conf.d/default.conf && mv /var/www/static-site/nginx.conf /etc/nginx/conf.d/default.conf
