FROM centos:centos6
MAINTAINER stormcat24 <a.yamada24@gmail.com>

# misc
RUN yum -y update
RUN yum install -y vim
RUN yum install -y git
RUN yum install -y java-1.7.0-openjdk

# aeromock-brew
RUN git clone https://github.com/CyberAgent/aeromock-brew.git
RUN cd aeromock-brew && \
    ./gradlew use -PaeromockVersion=0.2.3

# aeromock
ADD config.yaml /root/.aeromock/config.yaml
ADD project/project.yaml /project/project.yaml

ENTRYPOINT ~/.aeromock/applications/current/aeromock
EXPOSE 3183
