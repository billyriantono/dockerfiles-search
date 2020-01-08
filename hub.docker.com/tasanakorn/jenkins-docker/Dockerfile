FROM jenkins/jenkins:lts
USER root
RUN curl -sSL https://get.docker.com | sh
RUN usermod -aG docker jenkins
RUN curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash - && \
    sudo apt-get install -y nodejs && \
    sudo npm install -g newman
USER jenkins
