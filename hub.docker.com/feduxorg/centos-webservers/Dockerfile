FROM feduxorg/centos:latest
MAINTAINER dev@fedux.org

# ENV http_proxy http://172.17.42.1:3128
# ENV https_proxy https://172.17.42.1:3128

######
# APACHE
######

# Install and activate apache
RUN yum install -y httpd mod_ssl\
  && systemctl enable httpd \
  && yum clean -y all

# Setting up paths
RUN install -d /etc/httpd/sites-enabled \
    && install -d -g apache -m 0750 /etc/ssl/apache

# Setting up configuration
RUN rm -r /etc/httpd/conf.d/* \
    # Add Listener
    && sed -ri -e '/Listen 80/ a \Listen 443' /etc/httpd/conf/httpd.conf \
    # Modify DocumentRoot
    && sed -ri -e 's#/var/www/html#/srv/http#' /etc/httpd/conf/httpd.conf \
    && sed -ri -e 's#/var/www#/srv/http#' /etc/httpd/conf/httpd.conf \
    # Logs
    && sed -ri -e 's#logs/error_log#/var/log/httpd/error_log#' /etc/httpd/conf/httpd.conf \
    && sed -ri -e 's#logs/access_log#/var/log/httpd/access_log#' /etc/httpd/conf/httpd.conf \
    # Activate Event Worker
    && sed -ri -e '/mpm_prefork_module/s/LoadModule/#LoadModule/' /etc/httpd/conf.modules.d/00-mpm.conf \
    && sed -ri -e '/mpm_event_module/s/#LoadModule/LoadModule/' /etc/httpd/conf.modules.d/00-mpm.conf \
    # Add section to load enabled sites
    && sed -ri -e '$aIncludeOptional sites-enabled/*.conf' /etc/httpd/conf/httpd.conf

# Download configuration
RUN cd /tmp \
  && curl -L https://github.com/h5bp/server-configs-apache/archive/master.tar.gz | tar -xzf - -C .\
  && mv server-configs-apache-master/dist/.htaccess /etc/httpd/conf.d/h5bp.conf \
  && rm -r server-configs-apache-master/

# Add SSL/TLS configuration
ADD files/apache/ssl.conf /etc/httpd/conf.d/ssl.conf

ADD files/apache/ssl.example.com /etc/httpd/sites-enabled/ssl.example.com.conf
ADD files/ca/www.example.com.pem /etc/ssl/httpd/server.key
ADD files/ca/www.example.com.crt /etc/ssl/httpd/server.crt
ADD files/ca/www2.example.com.pem /etc/ssl/httpd/server2.key
ADD files/ca/www2.example.com.crt /etc/ssl/httpd/server2.crt
ADD files/ca/chain.crt /etc/ssl/httpd/chain.crt
ADD files/ca/chain2.crt /etc/ssl/httpd/chain2.crt

RUN chmod 0644 /etc/ssl/httpd/server.crt \
  && chmod 0644 /etc/ssl/httpd/chain.crt \
  && chmod 0640 /etc/ssl/httpd/server.key \
  && chown apache:apache /etc/ssl/httpd/server.*

# Activate Production Mode
RUN sed -ri -e 's/#ServerTokens/ServerTokens/' /etc/httpd/conf.d/h5bp.conf

# Expose ports
EXPOSE 80 443

######
# NGINX
######

# Install the Nginx.org CentOS repo.
ADD files/nginx/nginx.repo /etc/yum.repos.d/nginx.repo
ADD files/nginx/nginx.service /etc/systemd/system/nginx.service

# Install base stuff.
RUN yum -y install nginx \
  && systemctl enable nginx \
  && yum clean -y all

# Nginx config directories
RUN rm -rf /etc/nginx \
  && install -d /etc/nginx/sites-enabled \
  && install -d /srv/http \
  && install -d -o nginx -g nginx /var/log/nginx \
  && install -d -g nginx -m 0750 /etc/ssl/nginx \
  && install -d /etc/nginx/other-config \
  && cd /tmp \
  && curl -L https://github.com/h5bp/server-configs-nginx/archive/master.tar.gz | tar -xzf - -C . \
  && mv server-configs-nginx-master/* /etc/nginx/

ADD files/nginx/ssl.example.com /etc/nginx/sites-enabled/ssl.example.com.conf
ADD files/nginx/ssl.conf /etc/nginx/other-config/ssl.conf
ADD files/ca/www.example.com.pem /etc/ssl/nginx/server.key
ADD files/ca/server.crt /etc/ssl/nginx/server.crt
ADD files/ca/www2.example.com.pem /etc/ssl/nginx/server2.key
ADD files/ca/server2.crt /etc/ssl/nginx/server2.crt

# Output errors to stderr so that journald can grep them
RUN sed -ri 's#user www www;#user nginx nginx;#'  /etc/nginx/nginx.conf \
  && sed -ri '/user nginx nginx;/ a \ # Run nginx in foreground\ndaemon off;' /etc/nginx/nginx.conf \
  && sed -ri 's#logs/error.log#stderr#g' /etc/nginx/nginx.conf \
  && sed -ri 's#logs/access.log#/var/log/nginx/access.log#g' /etc/nginx/nginx.conf \
  && sed -ri '/static.log/ d' /etc/nginx/h5bp/location/expires.conf \
  && sed -ri '/access_log off/ d' /etc/nginx/h5bp/location/expires.conf \
  && chmod 0640 /etc/ssl/nginx/server.crt \
  && chown nginx:nginx /etc/ssl/nginx/server.crt

# Expose ports
EXPOSE 8080 8443

######
# COMMON
######

ADD files/ca/CA_Example_Com.crt /etc/pki/ca-trust/source/anchors/CA_Example_Com.crt
RUN chmod +r /etc/pki/ca-trust/source/anchors/CA_Example_Com.crt \
  && update-ca-trust extract

ADD files/index.htm /srv/http/index.html
RUN install -d -m 0755 /srv/http/getting_started/
ADD README.html /srv/http/getting_started/
ADD files/getting_started/index.html /srv/http/getting_started/
ADD files/ca/ /srv/http/getting_started/ca
RUN chmod -R +r /srv/http

# Working Directory
WORKDIR /
