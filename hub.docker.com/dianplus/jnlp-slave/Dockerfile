FROM jenkins/jnlp-slave:alpine
MAINTAINER Analyser <analyser@gmail.com>
LABEL Description="This is a base image, which allows connecting Jenkins agents via JNLP protocols" Vendor="DianPlus.cn"

ARG user=jenkins
ARG group=jenkins
ARG jk_home=/var/jenkins_home

USER root

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/' /etc/apk/repositories
RUN mkdir -p ${jk_home}/maven-prj-repos \
 && chown -R ${user}:${group} ${jk_home} \
 && apk add --no-cache maven apache-ant

USER ${user}
