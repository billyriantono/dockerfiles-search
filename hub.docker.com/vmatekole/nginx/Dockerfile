# Author Victor Matekole & Dockerfile
# Nginx Dockerfile
#
# Taken and amended from - https://github.com/dockerfile/nginx
#
# Pull base image.

FROM debian:8.0
MAINTAINER vmatekole
# Install Nginx.
RUN \ 
    apt-get update && \
    apt-get install -y make && \
    apt-get install -y build-essential && \
    apt-get install -y libpcre3-dev libpcre++-dev wget libssl-dev
RUN wget -P /tmp http://nginx.org/download/nginx-1.7.10.tar.gz && \
    tar -zxvf /tmp/nginx-1.7.10.tar.gz -C /tmp && \                  
    cd /tmp/nginx-1.7.10 && \
    ./configure  --prefix=/etc/nginx --sbin-path=/usr/sbin/nginx \
    --conf-path=/etc/nginx/nginx.conf --pid-path=/var/run/nginx.pid --lock-path=/var/run/nginx.lock \
    --error-log-path=/var/log/nginx/error.log \
    --http-log-path=/var/log/nginx/access.log \
    --user=nginx \
    --group=www-data \
    --with-http_ssl_module \
    --with-http_stub_status_module \
    --with-http_ssl_module \
    --with-http_gzip_static_module \
    --with-ipv6 \
    --with-http_realip_module 
RUN cd /tmp/nginx-1.7.10 && \
    make && \
    make install
RUN useradd nginx    
RUN chown -R www-data:www-data /etc/nginx

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log
# Define mountable directories.
VOLUME ["/etc/nginx" , "/etc/nginx/sites-enabled", "/etc/nginx/certs", "/etc/nginx/conf.d", "/var/log/nginx", "/var/www/html"]
# Define working directory.
WORKDIR /etc/nginx
# Define default command.
CMD ["nginx", "-g", "daemon off;"]
# Expose ports.
EXPOSE 80
EXPOSE 443