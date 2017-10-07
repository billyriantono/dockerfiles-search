FROM jenkins
MAINTAINER francois@garillot.net

# ENV TERM=xterm JENHOME=/var/jenkins_home JENREF=/usr/share/jenkins/ref
ENV TERM=xterm JENREF=/usr/share/jenkins/ref
USER root
RUN apt-get -qqy update \
    && apt-get install -qqy dnsutils build-essential libssl-dev openssl sudo \
    && echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers \
    && rm -rf /var/lib/apt/lists/*

############################################
# Configure Jenkins
############################################
# Switch to user jenkins
USER jenkins
# Jenkins settings
# COPY config/*.xml ${JENREF}/
# Define plugin set and run it's installation
COPY plugins.txt ${JENKINS_HOME}/plugins.txt
RUN /usr/local/bin/install-plugins.sh < ${JENKINS_HOME}/plugins.txt || exit 0
