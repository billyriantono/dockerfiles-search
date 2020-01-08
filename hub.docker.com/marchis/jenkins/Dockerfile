FROM jenkins/jenkins:lts

USER root

# Make root the owner of all files
RUN chown -R root "$JENKINS_HOME" /usr/share/jenkins/ref

RUN apt-get update && \
   apt-get -y install apt-transport-https \
       ca-certificates \
       curl \
       gnupg2 \
       software-properties-common && \
   curl -fsSL https://download.docker.com/linux/debian/gpg > /tmp/dkey; apt-key add /tmp/dkey && \
   add-apt-repository \
       "deb [arch=amd64] https://download.docker.com/linux/debian \
       $(lsb_release -cs) \
       stable" && \
   apt-get update && \
   apt-get -y install docker-ce

RUN apt-get install -y docker-ce
RUN usermod -a -G docker jenkins
USER jenkins