FROM centos:7

LABEL maintainer="matr1xc0in"

USER root

RUN rpm --import http://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-7

RUN curl --silent --location https://rpm.nodesource.com/setup_9.x | bash -

RUN yum clean all && rpm --rebuilddb && \
    yum -y install epel-release && \
    yum -y install \
    nodejs \
    unzip \ 
    nginx \
    && yum clean all && rm -rf /var/cache/yum

COPY remix-fa7ec31.zip /tmp/remix-ide.zip
RUN unzip -oq /tmp/remix-ide.zip -d /usr/share/nginx/html/ && \
    sed -i "/^[^#]*listen.*\[::\]:80 default_server;/ s/.*//" /etc/nginx/nginx.conf && \
    sed -i "/^[^#]*listen.*80 default_server/ s/.*/        listen 8080 default_server;/" /etc/nginx/nginx.conf

CMD ["nginx","-c","/etc/nginx/nginx.conf","-g","daemon off;"]
