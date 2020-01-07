FROM jenkins/jnlp-slave:latest
LABEL maintainer="peter@fixer.tech"
USER root

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
   apt-get -y install docker-ce && \
   usermod -aG docker jenkins

RUN curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash - && \
   apt-get install -y nodejs

RUN npm i -g @angular/cli

RUN wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.asc.gpg &&\
   sudo mv microsoft.asc.gpg /etc/apt/trusted.gpg.d/ && \
   wget -q https://packages.microsoft.com/config/debian/9/prod.list && \
   mv prod.list /etc/apt/sources.list.d/microsoft-prod.list && \
   chown root:root /etc/apt/trusted.gpg.d/microsoft.asc.gpg && \
   chown root:root /etc/apt/sources.list.d/microsoft-prod.list && \
   apt-get update && \
   apt-get -y install dotnet-sdk-2.2
