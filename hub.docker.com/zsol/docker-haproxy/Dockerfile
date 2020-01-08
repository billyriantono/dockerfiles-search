FROM haproxy:1.6

RUN apt-get update && apt-get install -y curl && \
    curl -LO https://github.com/jwilder/dockerize/releases/download/v0.0.4/dockerize-linux-amd64-v0.0.4.tar.gz && \
    tar -C /usr/local/bin -xzvf dockerize-linux-amd64-v0.0.4.tar.gz && \
    rm dockerize-linux-amd64-v0.0.4.tar.gz && apt-get clean

ADD haproxy.cfg.tmpl /haproxy.cfg.tmpl

CMD dockerize -template /haproxy.cfg.tmpl:/haproxy.cfg haproxy -db -f /haproxy.cfg
