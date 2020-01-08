# Dockerfile for Jenkins
# http://jenkins-ci.org/

FROM lucacesari/openjdk

MAINTAINER Luca Cesari <luc@cesari.me>

ENV JENKINS_USER jenkins
ENV JENKINS_HOME /srv/jenkins/jenkins

RUN pacman --noconfirm -Sqy --needed jenkins apache-ant maven git && \
    rm -r /var/cache/pacman/pkg && \
    rm -r /var/lib/pacman/sync

ADD run.sh /run.sh
RUN chmod 755 /run.sh

VOLUME ["/srv/jenkins"]
EXPOSE 8090

ENTRYPOINT ["/run.sh"]

