FROM centos:latest
LABEL maintainer="Igor Kolomiyets <igor.kolomiyets@iktech.io>"

RUN groupadd -g 10000 jenkins
RUN useradd -d /home/jenkins -g jenkins -u 10000 jenkins

RUN yum install -y rpm-build wget rpm-sign expect

USER 10000
RUN mkdir -p /home/jenkins/rpmbuild/{BUILD,RPMS,SOURCES,SPECS,SRPMS}

