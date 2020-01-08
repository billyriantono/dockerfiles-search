FROM curlimages/curl:latest
MAINTAINER Jesse DeFer <curl-ssh@dotd.com>

USER root

RUN adduser -D -u 1000 jenkins

RUN mkdir -p /home/jenkins/.ssh && chmod 0700 /home/jenkins/.ssh && echo -e "Host github.com\n\tStrictHostKeyChecking no\n" >> /home/jenkins/.ssh/config && chmod 0600 /home/jenkins/.ssh/config && chown -R jenkins:jenkins /home/jenkins/.ssh

RUN apk --no-cache add openssh-client 
