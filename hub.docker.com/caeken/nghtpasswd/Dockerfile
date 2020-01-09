FROM nginx:latest

ENV USERNAME=admin \
    PASSWORD=admin \
    PORT=80 \
    PROXY_PASS=http://127.0.0.1:8080
    
MAINTAINER Liu Chong <mail@clojure.cn>

RUN apt-get update && \
    apt-get dist-upgrade -y && \
    apt-get install --no-install-recommends -y apache2-utils && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ADD nginx.conf /etc/nginx/conf.d/default.conf

ADD start /usr/local/bin/start

CMD ["start"]
