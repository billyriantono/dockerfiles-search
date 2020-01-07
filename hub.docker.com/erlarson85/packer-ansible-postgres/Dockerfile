FROM bootswithdefer/packer-ansible 
MAINTAINER Erik Larson <packer-ansible@dotd.com>

ENV DOCKER_CHANNEL stable
ENV DOCKER_VERSION 18.09.1

RUN mkdir -p /home/jenkins/.ssh && chmod 0700 /home/jenkins/.ssh && echo -e "Host github.com\n\tStrictHostKeyChecking no\n" >> /home/jenkins/.ssh/config && chmod 0600 /home/jenkins/.ssh/config && chown -R jenkins:jenkins /home/jenkins/.ssh

RUN apk --no-cache add postgresql 
