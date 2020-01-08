FROM centos:7

MAINTAINER thedronzik <thedronzik@gmail.com>

ENV LUAJIT_VERSION 2.0.5
ENV NGINX_VERSION 1.13.5

# Set up ansible
RUN yum clean all && \
    yum -y install epel-release && \
    yum -y install PyYAML python-jinja2 python-httplib2 python-keyczar python-paramiko python-setuptools python-pip && \
    yum -y install cronie yum-cron

RUN mkdir /etc/ansible/ && \
    echo -e '[local]\nlocalhost' > /etc/ansible/hosts

RUN pip install --upgrade pip && \
    pip install ansible

# Add the ansible playbook
ADD ansible /srv/server

# Run the playbooks
RUN ansible-playbook /srv/server/server.yml -c local

#nginx
RUN mkdir -p /usr/local/src/luagit-2.0 && cd $_ && \
    curl -sL http://luajit.org/download/LuaJIT-${LUAJIT_VERSION}.tar.gz | tar xz --strip=1 && make && make install
RUN git clone git://github.com/simpl/ngx_devel_kit.git /usr/local/src/ngx_devel_kit && \
    git clone git://github.com/chaoslawful/lua-nginx-module.git /usr/local/src/lua-nginx-module && \
    curl -sL http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz | tar xz
RUN cd nginx-${NGINX_VERSION} && ./configure \
    --prefix=/usr \
    --conf-path=/etc/nginx/nginx.conf \
    --error-log-path=/var/log/nginx/error.log \
    --http-log-path=/var/log/nginx/access.log \
    --add-module=/usr/local/src/ngx_devel_kit \
    --add-module=/usr/local/src/lua-nginx-module \
    --with-file-aio \
    --with-ipv6 \
    --with-http_ssl_module \
    --with-http_v2_module \
    --with-http_realip_module \
    --with-http_addition_module \
    --with-http_sub_module \
    --with-http_mp4_module \
    --with-http_gunzip_module \
    --with-http_gzip_static_module \
    --with-http_auth_request_module \
    --with-http_random_index_module \
    --with-http_secure_link_module \
    --with-http_stub_status_module && make && make install

# Slim down the container
RUN yum clean all

# forward nginx and php-fpm request and error logs to docker log collector
RUN ln -sf /dev/stderr /var/log/nginx/error.log && \
    ln -sf /dev/stderr /var/log/nginx/access.log && \
    ln -sf /dev/stderr /var/log/php-fpm/error.log && \
    ln -sf /dev/stderr /var/log/php-fpm/www-error.log && \
    ln -sf /dev/stderr /var/log/php-fpm/www-slow.log

# Create site directory and set it as the default
RUN mkdir /app /etc/supervisord.d
WORKDIR /app
ENV APP_PATH /app

#ONBUILD ADD . /app

# expose ports
EXPOSE 80

# Add startup script
ADD ./start.sh /start.sh
RUN chmod 755 /start.sh


ADD ./export_envs.sh /export_envs.sh
RUN chmod 755 /export_envs.sh

# Execute start script
CMD ["/bin/bash", "/start.sh"]
