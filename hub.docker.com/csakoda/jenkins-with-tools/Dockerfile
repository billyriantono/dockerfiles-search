FROM jenkins
USER root
RUN apt-get update
RUN apt-get install mercurial -y
RUN curl https://get.docker.com/builds/Linux/x86_64/docker-1.8.3 -o /usr/bin/docker
RUN chmod +x /usr/bin/docker
USER jenkins
