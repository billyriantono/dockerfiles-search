FROM jenkins/jenkins

ENV DOCK_VER 18.03.1
USER root
RUN \
        curl https://download.docker.com/linux/static/stable/x86_64/docker-${DOCK_VER}-ce.tgz --output docker-${DOCK_VER}-ce.tgz && \
        tar xzvf docker-${DOCK_VER}-ce.tgz && \
        mv docker/docker /usr/local/bin/ && \
        rm docker-18.03.1-ce.tgz

EXPOSE 8080 50000
