FROM ubuntu:14.04
LABEL maintainer="tarlety@gmail.com"

RUN apt-get update \
 && apt-get install -y wget unzip \
 && apt-get install -y build-essential libpcre3 libpcre3-dev libssl-dev \
 && apt-get clean \
 && rm -r /var/lib/apt/lists/*

# build nginx with RTMP module
RUN mkdir -p /tmp/build && cd /tmp/build \
 && wget http://nginx.org/download/nginx-1.13.1.tar.gz \
 && tar -zxf nginx-1.13.1.tar.gz \
 && wget https://github.com/arut/nginx-rtmp-module/archive/v1.2.1.zip \
 && unzip v1.2.1.zip \
 && cd nginx-1.13.1 \
 && ./configure --with-http_ssl_module --add-module=../nginx-rtmp-module-1.2.1 \
 && make \
 && make install

# nginx configuration for rtmp
RUN rm /usr/local/nginx/html/*
RUN cp /tmp/build/nginx-rtmp-module-1.2.1/stat.xsl /usr/local/nginx/html
COPY nginx.conf /usr/local/nginx/conf/nginx.conf

# start nginx-rtmp
EXPOSE 1935
CMD ["/usr/local/nginx/sbin/nginx", "-g", "daemon off;"]
