FROM centos:centos6
MAINTAINER Dave Johnston email: dave.johnston@owmobility.com
WORKDIR /tmp

# Install Apache Web Server
RUN yum install -y httpd; yum clean all

# Add the tar file of the web site from my local directory
ADD test_content.tar /var/www/html/

EXPOSE 80
ENTRYPOINT [ "/usr/sbin/httpd" ]
CMD [ "-D", "FOREGROUND" ]
