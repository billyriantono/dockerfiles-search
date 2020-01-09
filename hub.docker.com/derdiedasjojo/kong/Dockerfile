FROM centos:7
MAINTAINER Jojo, jojo@openparse.io

ENV KONG_VERSION 0.9.3

RUN yum install -y wget https://github.com/Mashape/kong/releases/download/$KONG_VERSION/kong-$KONG_VERSION.el7.noarch.rpm && \
    yum clean all

RUN wget -O /usr/local/bin/dumb-init https://github.com/Yelp/dumb-init/releases/download/v1.1.3/dumb-init_1.1.3_amd64 && \
    chmod +x /usr/local/bin/dumb-init

#RUN mkdir -p /usr/local/kong/logs
#RUN ln -sf /dev/sterr /usr/local/kong/logs/error.log
#RUN ln -sf /dev/stdout /usr/local/kong/logs/access.log
env KONG_NGINX_DAEMON="off"

ADD piwik-log /usr/local/share/lua/5.1/kong/plugins/piwik-log/
ADD rate-limiting /usr/local/share/lua/5.1/kong/plugins/rate-limiting/

EXPOSE 8000 8443 8001 7946
CMD ["kong", "start"]
