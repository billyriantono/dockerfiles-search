FROM ghost:latest
MAINTAINER Ashik Patel <ashik@promactinfo.com>

RUN chown -R user:user /usr/src/ghost

# Add config and script to start the engine
ADD config.js /usr/src/ghost/config.js

RUN npm install -g pm2

RUN apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62
RUN echo "deb http://nginx.org/packages/mainline/debian/ jessie nginx" >> /etc/apt/sources.list

ENV NGINX_VERSION 1.9.6-1~jessie

RUN apt-get update && \
    apt-get install -y ca-certificates nginx=${NGINX_VERSION} && \
    rm -rf /var/lib/apt/lists/*

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

VOLUME ["/var/cache/nginx"]

EXPOSE 80 443

ADD entrypoint.sh /run-ghost.sh

RUN chmod 777 /run-ghost.sh 

CMD ["sh","/run-ghost.sh"]
