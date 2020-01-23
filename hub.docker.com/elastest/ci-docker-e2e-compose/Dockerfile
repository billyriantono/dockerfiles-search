FROM ubuntu:16.04
USER root

# Setup
RUN apt-get update && \
    apt-get install -y  software-properties-common\ 
    curl wget apt-transport-https build-essential git
    
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -

# Xvfb
RUN apt-get install -y xvfb supervisor
ENV DISPLAY :99.0
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
VOLUME /var/log/supervisord

# Java
# Java
RUN add-apt-repository ppa:openjdk-r/ppa
RUN apt-get update && apt-get install -y openjdk-8-jdk
# Define commonly used JAVA_HOME variable
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64

# Maven
RUN wget http://mirrors.viethosting.vn/apache/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz && \ 
    tar -xf apache-maven-3.3.9-bin.tar.gz  -C /usr/local
RUN ln -s /usr/local/apache-maven-3.3.9 /usr/local/maven
ENV M2_HOME /usr/local/maven
ENV PATH=${M2_HOME}/bin:${PATH}

# Chrome
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
  && echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list \
  && apt-get update -qqy \
  && apt-get -qqy install \
    google-chrome-stable \
  && rm /etc/apt/sources.list.d/google-chrome.list
COPY wrap_chrome_binary /opt/bin/wrap_chrome_binary
RUN chmod +x /opt/bin/wrap_chrome_binary
RUN /opt/bin/wrap_chrome_binary

# Firefox
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys AF316E81A155146718A6FBD7A6DCF7707EBC211F  \
  && echo "deb http://ppa.launchpad.net/ubuntu-mozilla-security/ppa/ubuntu trusty main" >> /etc/apt/sources.list.d/firefox.list \
  && apt-get update -qqy \
  && apt-get -qqy --no-install-recommends install \
    firefox \
  && rm -rf /etc/apt/sources.list.d/firefox.list

# Docker siblings
RUN add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
RUN apt-get update && \
    apt-get install -y docker-ce=5:18.09.1~3-0~ubuntu-xenial
RUN echo "export DOCKER_HOST='unix:///var/run/docker.sock'" >> /root/.bashrc \
 && echo "export DEBIAN_FRONTEND=noninteractive" >> /root/.bashrc

## Install DOCKER-COMPOSE 
RUN curl -L https://github.com/docker/compose/releases/download/1.23.2/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
RUN chmod +x /usr/local/bin/docker-compose

# Cleanup
RUN apt-get autoremove --purge

# Jenkins user
RUN useradd -ms /bin/bash jenkins &&\
    echo "jenkins:jenkins" | chpasswd
RUN usermod -aG docker jenkins
ENV WORKSPACE /home/jenkins
USER jenkins
WORKDIR ${WORKSPACE}

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
