## Build for AWS S3 Gitbook

FROM centos
## specify the group or individual maintaining image
MAINTAINER George Rolston <grolston@outlook.com>


## Update and install necessary pacakges.
RUN yum update -y
RUN yum install -y epel-release
RUN yum install -y awscli \
                   nodejs 
## setup gitbook
RUN npm install gitbook-cli -g
RUN gitbook fetch latest
RUN gitbook install
