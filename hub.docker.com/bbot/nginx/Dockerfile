FROM docker.io/centos

RUN yum install -y epel-release
RUN yum install -y nginx

RUN adduser -m -u 50000 docker

RUN sed -i 's/user nginx/user docker/g' /etc/nginx/nginx.conf
RUN sed -i 's#location / {#location / { autoindex on; auth_basic "Restricted"; auth_basic_user_file /auth/.htpasswd;#g' /etc/nginx/nginx.conf
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

EXPOSE 80


