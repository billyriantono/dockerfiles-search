#docker build -t unikum/buildenv -f buildenv_dockerfile .

FROM jenkins/jnlp-slave as slave

# Base image
FROM unikum/runtime-base

# Remember that the local docker group needs to have the same GID as the owning group of /var/run/docker.socket
# Horrible hack to set docker GID to same as host GID
RUN groupadd -g 502 docker

RUN yum update -y
RUN yum install -y https://centos7.iuscommunity.org/ius-release.rpm \
    && yum install -y git2u
#Install node, npm and yarn
RUN curl -sL https://rpm.nodesource.com/setup_9.x | bash - && \
        yum install -y nodejs-9.6.1 gcc-c++ make && \
    npm install --global yarn

# Install postgres client
RUN yum install -y postgresql

# Add packaged needed for docker repo
RUN yum install -y yum-utils \
      device-mapper-persistent-data \
      lvm2

# Add docker repo
RUN yum-config-manager \
        --add-repo \
        https://download.docker.com/linux/centos/docker-ce.repo

# Install docker
RUN yum install -y docker-ce

# Cleanup
RUN yum clean all

RUN mkdir -p /var/unikum/content/sitemap
RUN chown unikum /tmp
RUN chown -R unikum /var/unikum /home/unikum

RUN usermod -a -G docker unikum

USER unikum
WORKDIR /home/unikum

RUN mkdir /home/unikum/workspace
RUN mkdir /home/unikum/.gradle

ENV LC_ALL en_US.UTF-8

COPY --from=slave /usr/share/jenkins/slave.jar /usr/share/jenkins/slave.jar
COPY --from=slave /usr/local/bin/jenkins-slave /usr/local/bin/jenkins-slave
VOLUME /home/unikum/workspace
VOLUME /var/run/docker.sock

ENTRYPOINT ["jenkins-slave"]
