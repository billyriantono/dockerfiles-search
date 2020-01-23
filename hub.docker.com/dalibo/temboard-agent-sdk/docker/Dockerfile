FROM jenkins:2.0

# libapparmor-dev and libsystemd-journal0 are important to get docker in docker working

USER root
RUN apt-get update \
      && apt-get install -y sudo libapparmor-dev libsystemd-journal0 \
      && rm -rf /var/lib/apt/lists/*
RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers

USER jenkins
COPY plugins.txt /usr/share/jenkins/plugins.txt
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins.txt
