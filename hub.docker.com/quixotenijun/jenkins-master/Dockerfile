FROM  jenkins/jenkins:2.173-alpine
#FROM  jenkinsci/jenkins:2.154

# Jenkins image for CPE
#
# This image provides a Jenkins server, primarily intended for integration with
# FusiotnStage  CPE  2.2.1.
#
# Volumes:
# * /var/jenkins_home
# Environment:
# * $JENKINS_PASSWORD - Password for the Jenkins 'admin' user.

MAINTAINER nj.ni <nj.ni@huawei.com>

# Jenkins basic  image from
# https://hub.docker.com/r/jenkinsci/jenkins

ENV JENKINS_VERSION=2 \
#huawei build use rnd mirror,else use jenkins official
JENKINS_UC=https://updates.jenkins.io \
#JENKINS_UC=http://cmc-cd-mirror.rnd.huawei.com/jenkins-updates  \
CPE_JENKINS_IMAGE_VERSION=1.2.1 \
HUAWEI_FUSTIONSTAGE_CPE_VERSION=2.2.1 
LABEL k8s.io.description="Jenkins is a continuous integration server" \
k8s.io.display-name="Jenkins" \
cpe.io.expose-services="8080:http" \
cpe.io.tags="jenkins,ci" 

USER root

#RUN apt-get -o Acquire::Check-Valid-Until=false  update && apt-get install -y apt-transport-https  apt-utils  openssl && rm -rf /var/lib/apt/lists/*  \
#  && groupadd -g 1001 docker \
#  && usermod -a -G 1001 jenkins


#RUN   groupadd -g 1001 docker \
#  && usermod -a -G 1001,0 jenkins

COPY  init/jenkins  /usr/share/jenkins/ref

RUN chown -R 1000:0 /usr/share/jenkins/ref  \
  && /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins/base-plugins.txt  

USER jenkins
