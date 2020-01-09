# Based on the Fedora image created by Matthew Miller.
FROM centos:7
ARG TAG=8.0.7
RUN yum update -y && \
    yum install -y wget xmlstarlet java-1.8.0-openjdk-devel vim git rpm-build make && \
    wget https://packages.atlassian.com/atlassian-sdk-rpm/rpm-stable/atlassian-plugin-sdk-${TAG}.noarch.rpm && \
    yum localinstall -y atlassian-plugin-sdk-${TAG}.noarch.rpm && \
    rm atlassian-plugin-sdk-${TAG}.noarch.rpm && \
    yum clean all
