FROM docker:dind

RUN apk add --update openssh openrc bash openjdk8 git subversion wget

RUN     openrc \
        && touch /run/openrc/softlevel \
        && rc-update add sshd

RUN     adduser -D jenkins \
        && echo "jenkins:jenkins" | chpasswd \
        && echo "docker:x:999:jenkins" >> /etc/group

COPY dockerd-entrypoint.sh /usr/local/bin/dockerd-entrypoint.sh
