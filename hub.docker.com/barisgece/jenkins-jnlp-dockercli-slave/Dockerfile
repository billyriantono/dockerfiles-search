FROM barisgece/jenkins-jnlp-slave:latest

LABEL Baris Gece <gece.baris@gmail.com>

USER root

ARG DOCKER_CLI_VERSION="18.09.1"
ENV DOWNLOAD_URL="https://download.docker.com/linux/static/stable/x86_64/docker-$DOCKER_CLI_VERSION.tgz"

# Install Docker Client
RUN apt-get -qqy update \ 
    && mkdir -p /tmp/download \
    && curl -L $DOWNLOAD_URL | tar -xz -C /tmp/download \
    && mv /tmp/download/docker/docker /usr/local/bin/ \
    && rm -rf /tmp/download \
    && rm -rf /var/lib/apt/lists/*

USER jenkins

RUN mkdir -p /home/jenkins/.nuget/NuGet

COPY NuGet.Config /home/jenkins/.nuget/NuGet/
COPY my_password .

ENTRYPOINT [ "jenkins-slave" ]