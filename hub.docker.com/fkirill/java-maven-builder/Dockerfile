### Official image name cscope/java-maven-builder

FROM fkirill/sti-builder-java-maven-base

MAINTAINER Kirill Frolov <kirill.frolov@servian.com>

ADD sti/* /usr/local/sti/

ADD settings.xml $MAVEN_HOME/conf/

USER root

RUN chmod -R +x /usr/local/sti/*

USER 1001
