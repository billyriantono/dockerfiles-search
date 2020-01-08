FROM jenkins/ssh-slave

RUN apt-get update; \
    apt-get -y install apt-transport-https ca-certificates curl gnupg2 software-properties-common; \
    curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - ; \
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"; \
    apt-get update; \
    apt-get -y install docker-ce; \
    usermod -aG docker jenkins

COPY setup-docker-ssh-slave /usr/local/bin/setup-docker-ssh-slave

ENTRYPOINT ["setup-docker-ssh-slave"]
