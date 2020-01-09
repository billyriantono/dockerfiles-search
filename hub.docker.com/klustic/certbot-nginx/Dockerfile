FROM    debian:stretch-slim
EXPOSE  80/tcp 443/tcp
RUN     apt-get update && apt-get upgrade -y && apt-get autoremove -y && \
            apt-get install nginx python-certbot-nginx -y && \
            apt-get clean
COPY    resources/ /
CMD     /bin/bash /setup.sh
