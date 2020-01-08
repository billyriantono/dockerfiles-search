FROM centos:centos7
MAINTAINER Alfredo Matas "amatas@gmail.com"

# Enable EPEL for Node.js
RUN yum -y install epel-release
# Install Node.js and npm
RUN yum install -y npm nodejs-0.10.33 && yum clean all

CMD ["/bin/bash"]

