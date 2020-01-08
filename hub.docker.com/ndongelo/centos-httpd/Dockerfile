FROM centos
MAINTAINER Aurelio <aureliondongelo@gmail.com>
LABEL Vendor="CentOS"
LABEL License=GPLv2

RUN yum -y update && yum clean all &&\
yum -y install httpd &&\
yum -y install net-tools && yum clean all

EXPOSE 80

ADD run-httpd.sh /run-httpd.sh
RUN chmod -v +x /run-httpd.sh

CMD ["/run-httpd.sh"]
