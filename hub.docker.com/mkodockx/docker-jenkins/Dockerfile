FROM maven
MAINTAINER https://m-ko-x.de Markus Kosmal <code@m-ko-x.de>

ENV JENKINS_HOME /var/jenkins_home
ENV JENKINS_VERSION 1.651.2
ENV JENKINS_UC https://updates.jenkins-ci.org

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -y -q && apt-get install -y -q wget git curl zip npm && rm -rf /var/lib/apt/lists/*

RUN mkdir /usr/share/jenkins/
RUN useradd -d "$JENKINS_HOME" -u 1000 -m -s /bin/bash jenkins

RUN mkdir -p /usr/share/jenkins/ref/init.groovy.d
COPY init.groovy /usr/share/jenkins/ref/init.groovy.d/tcp-slave-angent-port.groovy

RUN curl -L http://mirrors.jenkins-ci.org/war/${JENKINS_VERSION}/jenkins.war -o /usr/share/jenkins/jenkins.war
RUN chown -R jenkins "$JENKINS_HOME" /usr/share/jenkins/ref

RUN mkdir -p /home/jenkins/.npm && mkdir -p /usr/local/lib/node_modules && mkdir -p /var/deploy
RUN chown -R jenkins /home/jenkins/.npm && chown -R jenkins /usr/local && chown -R jenkins /var/deploy
RUN ln -s /usr/bin/nodejs /usr/bin/node

VOLUME "${JENKINS_HOME}"

# for main web and slaves
EXPOSE 8080
EXPOSE 50000

USER jenkins

RUN npm install -g bower

COPY jenkins.sh /usr/local/bin/jenkins.sh
ENTRYPOINT ["/usr/local/bin/jenkins.sh"]