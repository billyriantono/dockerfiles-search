FROM debian:wheezy

RUN apt-key adv --keyserver pgp.mit.edu --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62 \
    && echo "deb http://nginx.org/packages/debian/ wheezy nginx" >> /etc/apt/sources.list \
    && apt-get update \
    && apt-get -y dist-upgrade \
    && apt-get install -y nginx \
    && apt-get clean \
    && apt-get autoclean \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/*
    
RUN apt-get update \
    && apt-get install -y curl ca-certificates --no-install-recommends \
    && curl -OSL https://github.com/st2py/nginx-hhvm/raw/master/html.tar.gz \
    && curl -OSL https://github.com/st2py/nginx-hhvm/raw/master/nginx.tar.gz \
    && rm -rf /etc/nginx \
    && tar -xzf nginx.tar.gz -C / \
    && tar -xzf html.tar.gz -C / \
    && rm nginx.tar.gz html.tar.gz \
    && apt-get purge -y --auto-remove curl ca-certificates \
    && apt-get clean \
    && apt-get autoclean \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/*
    
RUN touch /etc/run.sh \
    && chmod a+x /etc/run.sh \
    && echo "#!/bin/sh" > /etc/run.sh \
    && echo "" >> /etc/run.sh \
    && echo "/etc/init.d/nginx start" >> /etc/run.sh

EXPOSE 80 443

CMD ["/etc/run.sh"]
