FROM dockerfile/ubuntu
MAINTAINER Ryan Chipman

RUN add-apt-repository -y ppa:nginx/stable && \
    apt-get update && \
    apt-get install -y nginx && \
    chown -R www-data:www-data /var/lib/nginx && \
    rm -rf  /var/apt/lists/*

ADD ./nginx.conf /etc/nginx/nginx.conf

CMD ["nginx"]
EXPOSE 80
