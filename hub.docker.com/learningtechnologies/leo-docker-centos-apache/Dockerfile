FROM centos:latest

RUN yum install -y epel-release && \
    rpm -Uvh https://rhel7.iuscommunity.org/ius-release.rpm && \
    yum install -y httpd

EXPOSE 80

ENTRYPOINT ["/usr/sbin/httpd", "-D", "FOREGROUND"]