FROM jenkins
MAINTAINER Jevgeni Goloborodko <jevgeni@digital-magic.io>

USER root
#RUN apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
#RUN echo "deb https://apt.dockerproject.org/repo debian-jessie main" > /etc/apt/sources.list.d/docker.list
RUN curl -sSL https://get.docker.com/ | sh
RUN update-rc.d docker defaults
RUN apt-get install -y nano less
# TODO: Add jenkins to docker sudoers (see docker installer instructions): 
#usermod -aG docker jenkins
USER jenkins

COPY plugins.txt /usr/share/jenkins/ref/
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/ref/plugins.txt

USER root
ENV TERM=xterm
RUN gpasswd -a jenkins docker
RUN echo 'DOCKER_OPTS="--insecure-registry registry:5000"' >> /etc/default/docker
COPY entrypoint.sh /usr/local/bin/entrypoint.sh
ENTRYPOINT ["/bin/tini", "--", "/usr/local/bin/entrypoint.sh"]
