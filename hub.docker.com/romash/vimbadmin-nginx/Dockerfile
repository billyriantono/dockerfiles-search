FROM wodby/nginx:1.13
MAINTAINER Romash <tcp6000@gmail.com>

RUN rm /etc/gotpl/default-vhost.conf.tpl

COPY vimbadmin.conf.tpl /etc/gotpl/
COPY init/* /docker-entrypoint-init.d/



