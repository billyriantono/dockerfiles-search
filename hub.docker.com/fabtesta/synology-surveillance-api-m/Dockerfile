FROM fabric8/java-jboss-openjdk8-jdk:1.2
MAINTAINER Fabric8 Team <fabric8@googlegroups.com>

USER root

RUN yum -y -q install git which &&\
    yum clean all &&\
    git config --system user.name jboss &&\
    git config --system user.email jboss@localhost
    
USER jboss

