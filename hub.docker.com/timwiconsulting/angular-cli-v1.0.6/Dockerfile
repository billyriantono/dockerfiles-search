FROM ubuntu:trusty
MAINTAINER TIMWI <contact@timwi.com>

ENV DEBIAN_FRONTEND=noninteractive \
  NODE_VERSION=6.10.2 \
  SONAR_SCANNER=3.0.0.702-linux \
  SONAR_URL=http://localhost:9000 \
  DISPLAY=":1"

RUN echo '\nfs.inotify.max_user_watches=16384\n' >> /etc/sysctl.conf

# Set the timezone
RUN sudo echo "Europe/Paris" > /etc/timezone
RUN sudo dpkg-reconfigure -f noninteractive tzdata

# Setup environment
ENV PATH ${PATH}:/opt/sonar-scanner/bin

# Install basics & Java JDK
RUN apt-get update && apt-get install -y software-properties-common && \
  add-apt-repository ppa:webupd8team/java -y && \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
  apt-get update && \
  apt-get install -y git wget curl unzip bzip2 libfontconfig apt-transport-https oracle-java8-installer

# Get & Install NodeJS
RUN curl --retry 3 -SLO "http://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.gz" && \
  tar -xzf "node-v$NODE_VERSION-linux-x64.tar.gz" -C /usr/local --strip-components=1 && \
  rm "node-v$NODE_VERSION-linux-x64.tar.gz"

# Install Yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
  && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
  && apt-get update && apt-get install -y --force-yes yarn

# Install Angular-CLI
RUN yarn global add @angular/cli

#  Install Sonarqube scanner
RUN wget https://sonarsource.bintray.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-${SONAR_SCANNER}.zip && \
  unzip sonar-scanner-cli-${SONAR_SCANNER}.zip -d /opt && \
  rm sonar-scanner-cli-${SONAR_SCANNER}.zip && \
  mv /opt/sonar-scanner-${SONAR_SCANNER} /opt/sonar-scanner && \
  sed -i "s|#sonar.host.url=\(.*\)$|sonar.host.url=$SONAR_URL|" /opt/sonar-scanner/conf/sonar-scanner.properties && \
  chmod +x /opt/sonar-scanner/bin/sonar-scanner

# Install Google Chrome Browser
RUN wget -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
  echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list && \
  apt-get update -qqy && \
  apt-get -qqy install google-chrome-stable

RUN mkdir xnet

# Add xnet user
RUN useradd -ms /bin/bash xnet && \
  chown -Rf xnet xnet && \
  echo '\nPATH=${PATH}:/opt/sonar-scanner/bin\n' >> /home/xnet/.bashrc && \
  echo 'export PATH' >> /home/xnet/.bashrc && \
  echo '\nalias l="ls -lF"\nalias ll="ls -lAF"\n' >> /home/xnet/.bash_aliases

USER xnet

WORKDIR /home/xnet
EXPOSE 4200
EXPOSE 49152

ENTRYPOINT bash
