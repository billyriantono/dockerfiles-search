FROM openshift/base-centos7

LABEL maintainer="ChanGyu Seon <changyu.seon@bespinglobal.com>"

ENV NGINX_VERSION=1.6.3

LABEL io.k8s.description="Nginx webserver that build via npm" \
    io.k8s.display-name="Nginx 1.6.3 and npm builder" \
    io.openshift.expose-services="8080:http" \
    io.openshift.tags="builder,webserver,npm,webpack,nginx" \
    io.openshift.s2i.scripts-url="image:///usr/libexec/s2i"

RUN echo "NGINX_VERSION=${NGINX_VERSION}"

RUN yum install -y epel-release && \
    yum install -y --setopt=tsflags=nodocs nginx && \
    yum install -y --setopt=tsflags=nodocs nodejs && \
    yum clean all

RUN sed -i 's/80/8080/' /etc/nginx/nginx.conf
RUN sed -i 's/user nginx;//' /etc/nginx/nginx.conf
RUN sed -i 's/\/var\/log\/nginx\/error.log/stderr/' /etc/nginx/nginx.conf
RUN sed -i 's/access_log  \/var\/log\/nginx\/access.log  main;//' /etc/nginx/nginx.conf

COPY ./s2i/bin/ /usr/libexec/s2i

RUN chown -R 1001:1001 /usr/share/nginx
RUN chown -R 1001:1001 /var/log/nginx
RUN chown -R 1001:1001 /var/lib/nginx
RUN touch /run/nginx.pid
RUN chown -R 1001:1001 /run/nginx.pid
RUN chown -R 1001:1001 /etc/nginx

RUN chmod -R a+rx  /var/lib/nginx
RUN chmod -R a+rwx /var/lib/nginx/tmp
RUN chmod -R a+rwx /var/log/nginx
RUN chmod -R a+rwx /run

USER 1001

EXPOSE 8080

CMD ["/usr/libexec/s2i/usage"]
