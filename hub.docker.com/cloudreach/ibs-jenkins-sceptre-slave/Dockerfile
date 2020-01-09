FROM jenkinsci/slave:3.27-1-alpine
LABEL Description="Cloudreach Sceptre Deployer"
LABEL Maintainer="Ruben Sancho <ruben.sancho@cloudreach.com>"

USER root
RUN apk add --update --no-cache curl py-pip python3 && \
    pip3 install awscli troposphere sceptre==2.0.1 netaddr && \
    apk --purge -v del py-pip && \
    rm -f /var/cache/apk/*
USER jenkins
COPY jenkins-slave /usr/local/bin/jenkins-slave

ENTRYPOINT ["/usr/local/bin/jenkins-slave"]