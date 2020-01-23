FROM centos:centos7
RUN yum install -y httpd && \
    yum clean all
CMD ["/usr/sbin/httpd", "-DFOREGROUND"]
EXPOSE 80
