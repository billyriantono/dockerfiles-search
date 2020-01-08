FROM centos:7

MAINTAINER "Carlos H Brandt <carloshenriquebrandt.gmail>"

RUN yum -y install vim git tar wget curl which tcsh &&\
    yum clean all

RUN git clone -b stable https://github.com/chbrandt/docker_commons.git && \
    ln -sf docker_commons/entrypoint.sh /.

ENTRYPOINT ["/entrypoint.sh"]
