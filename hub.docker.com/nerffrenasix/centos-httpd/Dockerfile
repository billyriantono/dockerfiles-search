FROM centos
MAINTAINER nerffren
RUN yum -y update
RUN yum -y install httpd
RUN systemctl enable httpd
CMD ["systemctl","enable","httpd"]
