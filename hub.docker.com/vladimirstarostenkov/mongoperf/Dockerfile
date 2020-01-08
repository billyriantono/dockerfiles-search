FROM centos:7

COPY mongodb.repo /etc/yum.repos.d/
RUN yum install -y mongodb-org-tools

WORKDIR /tmp
ENTRYPOINT [ "mongoperf" ]
