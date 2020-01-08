FROM jenkins/jenkins:lts
USER root
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN cat /usr/share/jenkins/ref/plugins.txt | /usr/local/bin/install-plugins.sh


RUN apt-get update && \
 apt-get -y install apt-transport-https \
     ca-certificates \
     curl \
     gnupg2 \
     software-properties-common && \
 curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg > /tmp/dkey; apt-key add /tmp/dkey && \
 add-apt-repository \
 "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
   $(lsb_release -cs) \
   stable" && \
 apt-get update && \
 apt-get -y install docker-ce
 
ENTRYPOINT ["/sbin/tini", "--", "/usr/local/bin/jenkins.sh"]
