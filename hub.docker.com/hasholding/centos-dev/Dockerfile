FROM centos:7
MAINTAINER "Levent SAGIROGLU" <LSagiroglu@gmail.com>

RUN yum -y update ;\
    yum -y install wget nano openssl ;\
	yum -y group install "Development Tools" ;\
    yum clean all

VOLUME /workdir
WORKDIR /workdir

CMD ["/bin/bash"]
