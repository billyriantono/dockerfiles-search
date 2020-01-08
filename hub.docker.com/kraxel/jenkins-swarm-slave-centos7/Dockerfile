FROM centos:centos7

ENV OPENJDK_VERSION="1.8.0" \
    SWARM_CLIENT_VERSION="3.17" \
    SUMMARY="jenkins swarm client" \
    DESCRIPTION="jenkins swarm client for rpm package builds" \
    TAGS="jenkins"

LABEL maintainer="Gerd Hoffmann <kraxel@redhat.com>" \
      summary="${SUMMARY}" \
      description="${DESCRIPTION}" \
      io.k8s.display-name="${SUMMARY}" \
      io.k8s.description="${DESCRIPTION}" \
      io.openshift.tags="${TAGS}"

USER root

RUN yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm; \
    yum repolist; \
    yum install -y java-${OPENJDK_VERSION}-openjdk-headless \
                   wget sudo git bc which make \
                   fedpkg mock rpm-build tito \
                   ; \
    yum clean all -y

RUN useradd --user-group --groups wheel,mock jenkins
COPY sudo* /etc/sudoers.d/
USER jenkins

WORKDIR /home/jenkins
COPY swarm-client.sh .
RUN wget https://repo.jenkins-ci.org/releases/org/jenkins-ci/plugins/swarm-client/${SWARM_CLIENT_VERSION}/swarm-client-${SWARM_CLIENT_VERSION}.jar; \
    chmod a+r . swarm*; \
    chmod a+w .; \
    chmod a+x . *.sh; \
    echo "---"; \
    ls -la; \
    echo "---"; \
    id -a; \
    echo "---"

CMD ["/home/jenkins/swarm-client.sh"]
