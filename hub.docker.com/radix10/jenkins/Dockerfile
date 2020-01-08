# Customized jenkins image
FROM jenkins/jenkins:lts
MAINTAINER "admin@radix10.cn"

# Install plugins
RUN /usr/local/bin/install-plugins.sh \
cloudbees-folder \
antisamy-markup-formatter \
build-timeout \
credentials-binding \
timestamper \
ws-cleanup \
ant \
gradle \
workflow-aggregator \
github-branch-source \
pipeline-github-lib \
pipeline-stage-view \
git \
subversion \
ssh-slaves \
matrix-auth \
pam-auth \
ldap \
email-ext \
mailer \
localization-zh-cn \
docker-plugin \
blueocean

# Install docker
USER root
RUN curl -sSL https://get.docker.com | sh
USER jenkins
