FROM nginx
RUN apt update && apt install -y \
    wget curl iputils-ping telnet net-tools procps vim mc nano \
    && sed -ie "s/user[ ]*nginx/user www-data/g" /etc/nginx/nginx.conf
