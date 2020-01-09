FROM ubuntu:zesty
MAINTAINER TIMWI <contact@timwi.com>

ENV DEBIAN_FRONTEND=noninteractive \
  NODE_VERSION=8.2.1 \
  SONAR_SCANNER=3.0.0.702-linux \
  SONAR_URL=http://localhost:9000

# Setup environment
ENV PATH ${PATH}:/opt/sonar-scanner/bin

# Install basics & Java JDK 8
RUN apt-get update && apt-get install -y software-properties-common && \
  add-apt-repository ppa:webupd8team/java -y && \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
  apt-get update && \
  apt-get install -y git wget curl unzip bzip2 libfontconfig apt-transport-https python python-dev build-essential && \
  apt-get install -y oracle-java8-installer

#  Install Sonarqube scanner
RUN wget https://sonarsource.bintray.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-${SONAR_SCANNER}.zip && \
  unzip sonar-scanner-cli-${SONAR_SCANNER}.zip -d /opt && \
  rm sonar-scanner-cli-${SONAR_SCANNER}.zip && \
  mv /opt/sonar-scanner-${SONAR_SCANNER} /opt/sonar-scanner && \
  sed -i "s|#sonar.host.url=\(.*\)$|sonar.host.url=$SONAR_URL|" /opt/sonar-scanner/conf/sonar-scanner.properties && \
  chmod +x /opt/sonar-scanner/bin/sonar-scanner

# Get & Install NodeJS
RUN curl --retry 3 -SLO "http://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.gz" && \
  tar -xzf "node-v$NODE_VERSION-linux-x64.tar.gz" -C /usr/local --strip-components=1 && \
  rm "node-v$NODE_VERSION-linux-x64.tar.gz"

# Add generic-user user
RUN mkdir generic-user
RUN useradd -ms /bin/bash generic-user && \
  chown -Rf generic-user generic-user && \
  echo '\nPATH=${PATH}:/opt/sonar-scanner/bin\n' >> /home/generic-user/.bashrc && \
  echo 'export PATH' >> /home/generic-user/.bashrc && \
  echo '\nalias l="ls -lF"\nalias ll="ls -lAF"\n' >> /home/generic-user/.bash_aliases

COPY .npmrc /home/generic-user/.npmrc
RUN chown generic-user /home/generic-user/.npmrc

USER generic-user

WORKDIR /home/generic-user

ENTRYPOINT bash
