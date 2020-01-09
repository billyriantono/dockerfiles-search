FROM centos:7
LABEL maintainer="felix.koppe@cavorit.de"
ENV container docker

RUN yum install -y epel-release
RUN yum install -y java-1.8.0-openjdk-headless maven nodejs git createrepo rpm-build yum-utils zip unzip

CMD ["bash"]
