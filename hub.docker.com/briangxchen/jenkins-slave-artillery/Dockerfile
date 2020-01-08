FROM openshift/jenkins-slave-base-centos7

LABEL org.centos.component="jenkins-slave-artillery" \
      name="jenkins-slave-artillery" \
      architecture="x86_64" \
      io.k8s.display-name="Jenkins Slave artillery" \
      io.k8s.description="Artillery tools on top of the jenkins slave base image" \
      io.openshift.tags="openshift,jenkins,slave,load"
USER root

RUN curl -sL https://rpm.nodesource.com/setup_8.x | bash -

RUN yum install nodejs -y
RUN yum install epel-release -y
RUN yum install jq -y
RUN yum install -y git bzip2

RUN npm install -g artillery --allow-root --unsafe-perm=true

RUN yum -y --setopt=tsflags=nodocs update && \
    yum -y --setopt=tsflags=nodocs install socat && \
    yum -y --setopt=tsflags=nodocs install wget && \
    yum -y --setopt=tsflags=nodocs install git && \
    yum -y --setopt=tsflags=nodocs install tmux && \
    wget https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm && \
    yum -y install ./google-chrome-stable_current_x86_64.rpm
RUN npm install -g chrome-headless-render-pdf
RUN npm install -g node-localstorage

RUN yum clean all
RUN google-chrome --version
RUN node --version
RUN npm --version

USER 1001
