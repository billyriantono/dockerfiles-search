FROM jenkins/jenkins:lts-alpine
RUN /usr/local/bin/install-plugins.sh \
  kubernetes:1.12.7 \
  workflow-job:2.26 \
  workflow-aggregator:2.6 \
  credentials-binding:1.16 \
  git:3.9.1
