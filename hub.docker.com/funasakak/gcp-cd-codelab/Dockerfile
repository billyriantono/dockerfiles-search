#FROM alpine
#
#COPY gopath/bin/gcp-cd-codelab /go/bin/gcp-cd-codelab
#
#ENTRYPOINT /go/bin/gcp-cd-codelab
FROM centos:centos6
ENV container docker
RUN yum install -y epel-release && \
    yum install -y nginx && \
    yum clean all && \
    echo "test page 20180324 17:18" > /usr/share/nginx/html/index.html
ENTRYPOINT /usr/sbin/nginx -g 'daemon off;' -c /etc/nginx/nginx.conf
EXPOSE 80

