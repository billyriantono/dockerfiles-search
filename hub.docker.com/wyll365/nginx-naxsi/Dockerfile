FROM ubuntu:trusty

MAINTAINER AdinZ <1454269@qq.com>


#Software versions
ENV NGINX_VERSION 1.9.10
ENV NAXSI_VERSION master

#Install needed packages from repos
RUN apt-get update &&\
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
					    wget python-pip python-geoip logtail curl \
					    gcc make libpcre3-dev libssl-dev \
					    supervisor

#Get nginx and naxsi-ui
RUN cd /usr/local/ && \
    wget "http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz" && \
    wget "https://github.com/nbs-system/naxsi/archive/${NAXSI_VERSION}.tar.gz" && \
    tar zxvf nginx-${NGINX_VERSION}.tar.gz && \
    tar zxvf ${NAXSI_VERSION}.tar.gz

#Build and install nginx + naxsi
RUN cd /usr/local/nginx-${NGINX_VERSION}/ && \
    ./configure \
      --conf-path=/etc/nginx/nginx.conf --add-module=../naxsi-${NAXSI_VERSION}/naxsi_src/ \
      --error-log-path=/var/log/nginx/error.log --http-client-body-temp-path=/var/lib/nginx/body \
      --http-fastcgi-temp-path=/var/lib/nginx/fastcgi --http-log-path=/var/log/nginx/access.log \
      --http-proxy-temp-path=/var/lib/nginx/proxy --lock-path=/var/lock/nginx.lock \
      --pid-path=/var/run/nginx.pid --with-http_ssl_module \
      --without-mail_pop3_module --without-mail_smtp_module \
      --without-mail_imap_module --without-http_uwsgi_module \
      --without-http_scgi_module --with-ipv6 --prefix=/usr && \
     make && \
     make install 

# #Install nxapi / nxtool
RUN cd /usr/local/naxsi-${NAXSI_VERSION} && \
     cp naxsi_config/naxsi_core.rules /etc/nginx/ 
#      cd nxapi && \
#      pip install -r requirements.txt && \
#      python setup.py install

#Configuration files
ADD nginx/nginx.conf /etc/nginx/nginx.conf
ADD naxsi/naxsi.rules /etc/nginx/naxsi.rules
ADD naxsi/nxapi.json /usr/local/etc/nxapi.json
RUN mkdir /etc/nginx/naxsi-local-rules
RUN mkdir -p /var/lib/nginx/body



#Ports
EXPOSE 80

ENTRYPOINT ["nginx", "-g", "daemon off;"]


