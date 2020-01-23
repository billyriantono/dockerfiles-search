FROM tomcat:alpine

MAINTAINER Chen Augus <tianhao.chen@gmail.com>

RUN cd /tmp && \
    wget -c https://github.com/psi-probe/psi-probe/releases/download/3.1.0/probe.war && \
    mv probe.war /usr/local/tomcat/webapps/
