FROM phusion/baseimage:0.9.19

COPY . /app
WORKDIR /app

RUN \
    apt-get update && \
    apt-get install -y \
        nginx \
        git \
        wget \
        gettext \
    && \
    apt-get clean

#make nginx not run as a daemon so it doesn't exit at entrypoint
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

ADD startservices.sh /usr/bin/startservices.sh

RUN chmod +x /usr/bin/startservices.sh

ADD nginx.conf.template /etc/nginx/nginx.conf.template

CMD /usr/bin/startservices.sh