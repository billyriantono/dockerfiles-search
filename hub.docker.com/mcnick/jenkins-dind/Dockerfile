FROM jenkins:2.0
 
USER root
RUN apt-get update \
    && apt-get install -y curl lib32z1 lib32ncurses5 gcc gcc-multilib
RUN curl -sSL https://get.docker.com/ | sh
RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers
RUN gpasswd -a jenkins docker
RUN gpasswd -a root docker
RUN usermod -aG docker jenkins

USER jenkins
