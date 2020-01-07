FROM centos:7

MAINTAINER victor@vrdominguez.es

RUN yum update -y && yum install -y epel-release && yum install -y ansible

ENTRYPOINT ["/usr/bin/ansible"]

CMD ["--help"]
