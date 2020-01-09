FROM nginx:1.12

RUN apt-get update && apt-get install -y apache2-utils
ENV RAILS_ROOT /var/www/sub_project
WORKDIR $RAILS_ROOT
ADD nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD [ "nginx", "-g", "daemon off;" ]

