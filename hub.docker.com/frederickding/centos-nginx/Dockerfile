FROM centos:centos7

# import GPG signing key
ADD etc/pki/rpm-gpg/RPM-GPG-KEY-nginx /etc/pki/rpm-gpg/RPM-GPG-KEY-nginx
RUN rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-nginx

# install package
ADD etc/yum.repos.d/nginx-mainline.repo /etc/yum.repos.d/nginx-mainline.repo
RUN yum install -y nginx patch

# apply patched configuration
ADD etc/nginx/nginx.conf.patch /etc/nginx/nginx.conf.patch
RUN patch /etc/nginx/nginx.conf < /etc/nginx/nginx.conf.patch

# we can't manually update a version number on every build
ENV NGINX_BRANCH mainline

RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

VOLUME ["/var/cache/nginx"]

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
