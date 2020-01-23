FROM jenkins/jenkins:lts
#host docker group id
#ARG GROUD_ID=1009
USER root
RUN apt-get update -y \
      && apt-get install -y sudo \
      && rm -rf /var/lib/apt/lists/*
#add jenkins to sudoers
RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers
#add user jenkins to docker group
#RUN echo "docker:x:${GROUP_ID}:jenkins" >> /etc/group
USER jenkins
