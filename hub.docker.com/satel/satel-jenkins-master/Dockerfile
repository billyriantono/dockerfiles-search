FROM jenkins/jenkins:2.150.1

# Root is required to modify uid
USER root

# Setup specific to our server
RUN usermod --uid 1003 jenkins
RUN groupadd -g 995 docker
RUN usermod -a -G docker jenkins
RUN groupmod --gid 1002 jenkins
RUN chown -R jenkins:jenkins "$JENKINS_HOME" /usr/share/jenkins/ref

# Install the latest Docker CE binaries
RUN apt-get update
RUN apt-get -y install apt-transport-https ca-certificates curl gnupg2 software-properties-common
RUN curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg > /tmp/dkey
RUN apt-key add /tmp/dkey
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") $(lsb_release -cs) stable"
RUN apt-get update
RUN apt-get -y install docker-ce python3-pip
# RUN curl -L https://github.com/docker/compose/releases/download/1.19.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
# RUN chmod +x /usr/local/bin/docker-compose
RUN pip3 install docker-compose
RUN curl -L https://github.com/docker/machine/releases/download/v0.14.0/docker-machine-`uname -s`-`uname -m` >/usr/local/bin/docker-machine && chmod +x /usr/local/bin/docker-machine

# restore ENTRYPOINT to startup as jenkins user
USER jenkins
