FROM jenkins/jnlp-slave
LABEL MAINTAINER="ZhuJun Lu <24comic@gmail.com>"

USER root
RUN curl -sL https://deb.nodesource.com/setup_8.x | /bin/bash - \
  && apt-get install -y nodejs sudo \
  && apt-get clean \
  && echo 'jenkins ALL= (root) NOPASSWD: /usr/bin/n' >> /etc/sudoers \
  && echo 'jenkins ALL= (root) NOPASSWD: /usr/bin/npm' >> /etc/sudoers \
  && echo 'jenkins ALL= (root) NOPASSWD: /usr/bin/yarn' >> /etc/sudoers \
  && npm install -g n yarn \
  && chown jenkins:jenkins -R /home/jenkins/

USER jenkins
