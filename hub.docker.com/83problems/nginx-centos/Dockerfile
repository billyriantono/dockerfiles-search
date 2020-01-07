FROM centos:7

ARG NGINX_VERSION=1.12.0

LABEL name="nginx-centos" \ 
      description="NGINX ${NGINX_VERSION} running on CentOS 7." \
      maintainer="Brian Gribble <brian@83problems.com>"

ENV NGINX_REPO_RPM nginx-release-centos-7-0.el7.ngx.noarch.rpm

# Install nginx
RUN /usr/bin/curl -L http://nginx.org/packages/centos/7/noarch/RPMS/${NGINX_REPO_RPM} -o /tmp/${NGINX_REPO_RPM}
RUN /usr/bin/yum -y update \
    && /usr/bin/yum -y install /tmp/${NGINX_REPO_RPM} \
    && /usr/bin/yum -y install nginx-${NGINX_VERSION} \
    && /usr/bin/yum clean all

# Remove RPM
RUN /bin/rm /tmp/${NGINX_REPO_RPM}

# Directory for nginx temp files
RUN /bin/mkdir /tmp/nginx
RUN /bin/chown nginx:nginx /tmp/nginx

# Copy custom nginx.conf
COPY files/nginx.conf /etc/nginx/

RUN /bin/echo "NGINX ${NGINX_VERSION} on CentOS 7" > /usr/share/nginx/html/index.html

EXPOSE 80

USER 998

CMD [ "nginx" ]
