FROM jenkins/jenkins:lts-slim


USER jenkins

ENV JENKINS_REF "/usr/share/jenkins/ref"
ENV JENKINS_TIMEZONE "America/Sao_Paulo"

ENV JENKINS_MAVEN_ENABLED true
ENV JENKINS_MAVEN_VERSION 3.5.4

#COPY jenkins-home/maven/.m2/settings.xml $JENKINS_REF/apache-maven/apache-maven-$JENKINS_MAVEN_VERSION/.m2/settings.xml
COPY jenkins-home/maven/.m2/settings.xml ~/.m2/settings.xml
COPY jenkins-home/.ssh ~/.ssh/

COPY jenkins-home/.aws ~
COPY jenkins-home/scripts/reload-aws-ecr-credential.sh ~


USER root

COPY rancher /usr/bin
RUN chmod +x /usr/bin/rancher


RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    build-essential \
    python-pip \
    python-dev \
    nmap \
    nano \
    cron \
    wget \
    curl \
    awscli

RUN curl -fsSL https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
    echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list && \
    apt-get update && \
    apt-get install -y --no-install-recommends google-chrome-stable

RUN echo $JENKINS_TIMEZONE > /etc/timezone && \
		rm /etc/localtime && \
		dpkg-reconfigure -f noninteractive tzdata

RUN wget https://releases.rancher.com/install-docker/17.06.sh && \
		chmod 700 17.06.sh && \
		./17.06.sh && \
		usermod -aG docker jenkins

COPY jenkins-home/scripts/reload-token-aws /etc/cron.d/reload-token-aws
RUN chmod 0644 /etc/cron.d/reload-token-aws && \
		cron


USER jenkins

ENV RANCHER_ACCESS_KEY  "key"
ENV RANCHER_SECRET_KEY  "secret"
ENV RANCHER_URL "http://rancher:8080/v1"

ENV JENKINS_EMAIL_REPLY_TO "jenkins@sinistroauto.com"
ENV JENKINS_EMAIL_HOST "localhost"
ENV JENKINS_EMAIL_AUTH_USER "user"
ENV JENKINS_EMAIL_AUTH_SECRET "secret"
ENV JENKINS_EMAIL_SMTP_PORT "123"

ENV JENKINS_PUBLIC_URL "http://localhost:8080/"

ENV JENKINS_EMAIL_ADMIN_ADDRESS "jenkins@sinistroauto.com"
ENV JENKINS_GIT_CONFIG_NAME "jenkins"
ENV JENKINS_GIT_CONFIG_EMAIL "jenkins@sinistroauto.com"
ENV JENKINS_USERNAME "admin"
ENV JENKINS_PASSWORD "admin"

ENV JAVA_OPTS -Dorg.eclipse.jetty.server.Request.maxFormContentSize=100000000 \
		-Dorg.apache.commons.jelly.tags.fmt.timeZone=$JENKINS_TIMEZONE \
		-Dhudson.diyChunking=false \
		-Djenkins.install.runSetupWizard=false \
		-Dmail.smtp.starttls.enable=true \
		-Djava.awt.headless=true \
		-Djenkins.install.runSetupWizard=false

ENV BUILD_ENV "dsv"
ENV DOCKER_HOST "tcp://10.0.0.0:2375"

ENV JENKINS_SONAR_SERVER_URL "http://10.0.0.0:9000/"
ENV JENKINS_SONAR_PLUGIN_VERSION ""
ENV JENKINS_SONAR_ADDITIONAL_PROPS ""
ENV JENKINS_SONAR_RUNNER_VERSION 6.5.0

ENV JENKINS_ARTIFACTORY_URL "http://artifactory:8081"
ENV JENKINS_ARTIFACTORY_SERVER_ID "artifactory"
ENV JENKINS_ARTIFACTORY_USER "admin"
ENV JENKINS_ARTIFACTORY_PASSWORD "password"

ENV JENKINS_MVN_REGISTRY_ID "docker-registry"
ENV JENKINS_MVN_REGISTRY_USERNAME "user"
ENV JENKINS_MVN_REGISTRY_PASSWORD "pass"
ENV JENKINS_MVN_REGISTRY_EMAIL "jenkins@sinistroauto.com"

ENV JENKINS_NODEJS_VERSION "8.15.0"
ENV JENKINS_NODEJS_GLOBAL_PACKAGES ""
ENV JENKINS_NODEJS_PACKAGES_REFRESH_HOURS 72

COPY python_libs.txt /
RUN cd / && \
		pip install -r python_libs.txt

# install jenkins plugins
COPY jenkins-home/plugins.txt $JENKINS_REF/plugins.txt
RUN /usr/local/bin/install-plugins.sh < $JENKINS_REF/plugins.txt
#COPY jenkins-home/plugins $JENKINS_REF/plugins/

# copy scripts and resource files
COPY jenkins-home/*.* $JENKINS_REF/
COPY jenkins-home/jobs $JENKINS_REF/jobs/
COPY jenkins-home/init.groovy.d $JENKINS_REF/init.groovy.d/
