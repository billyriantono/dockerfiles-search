FROM 4devs/centos

ADD yum.repos.d/nginx.repo /etc/yum.repos.d/nginx.repo

RUN yum install -y --setopt=tsflags=nodocs nginx \
  && yum clean all \
  && mkdir -p /usr/share/nginx/html \
  && rm -f /etc/nginx/conf.d/default.conf

ADD root /

RUN echo "nginx on CentOS7" > /usr/share/nginx/html/index.html

EXPOSE 80 443

CMD ["nginx"]
