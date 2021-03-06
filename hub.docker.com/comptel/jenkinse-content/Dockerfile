FROM jenkins/jenkins:lts

LABEL MAINTAINER="codeontap"

#Copy Jenkins init files - make sure they override the old files
COPY scripts/init/ /usr/share/jenkins/ref/init.groovy.d/
RUN find /usr/share/jenkins/ref/init.groovy.d/ -type f -exec mv '{}' '{}'.override \;

# install plugins specified in https://github.com/kohsuke/jenkins/blob/master/core/src/main/resources/jenkins/install/platform-plugins.json
COPY scripts/plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

COPY scripts/log.properties /usr/share/jenkins/ref/log.properties

# Container Configuration 
USER root

# Create extra volumes for logging and WAR cache location to allow for updates as part of master docker image 
RUN mkdir /var/log/jenkins
RUN mkdir /var/cache/jenkins
RUN chown -R jenkins:jenkins /var/log/jenkins
RUN chown -R jenkins:jenkins /var/cache/jenkins

# Install OS Packages
RUN apt-get update && apt-get install -y \
    curl \
    apt-utils \
    dos2unix \
    tar zip unzip \
    less vim tree \
    git \
    jq \
 && rm -rf /var/lib/apt/lists/*

# Change back to jenkins user to run jenkins
USER jenkins

ENV JENKINS_URL=""
ENV JENKINSLB_URL=""

ENV JENKINSENV_SLAVEPROVIDER="ecs"

# Jenkins Authentication
ENV JENKINSENV_SECURITYREALM="local"

ENV JENKINSENV_USER=""
ENV JENKINSENV_PASS=""

ENV GITHUBAUTH_CLIENTID=""
ENV GITHUBAUTH_ADMIN=""
ENV GITHUBAUTH_SECRET=""

ENV AGENT_REMOTE_FS="/home/jenkins"

ENV TIMEZONE="Australia/Sydney"
ENV MAXMEMORY="4096m"
ENV JAVA_OPTS="-Dhudson.DNSMultiCast.disabled=true \
                -Djenkins.install.runSetupWizard=false \
                -Djava.util.logging.config.file=/usr/share/jenkins/ref/log.properties \
                -Dorg.apache.commons.jelly.tags.fmt.timeZone=${TIMEZONE} \
                -Duser.timezone=${TIMEZONE} \
                -Xmx${MAXMEMORY} \
                -Dhudson.slaves.ChannelPinger.pingIntervalSeconds=300 -Dhudson.slaves.ChannelPinger.pingTimeoutSeconds=30 ${JAVA_EXTRA_OPS}"

# Set environmental configuration for Jenkins
ENV JENKINS_OPTS="--logfile=/var/log/jenkins/jenkins.log --webroot=/var/cache/jenkins/war"
