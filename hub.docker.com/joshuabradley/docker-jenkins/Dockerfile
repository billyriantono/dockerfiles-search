FROM jenkins/jenkins:2.117-slim
LABEL maintainer "Joshua Bradley <josh@joshuabradley.io>"
LABEL service-name "datapp-jenkins"

# declare build time arguments
ARG ENV_TZ="US/Pacific"

# set timezone for Jenkins container
USER root
ENV JENKINS_TZ=$ENV_TZ
RUN echo $JENKINS_TZ > /etc/timezone
USER jenkins

# install custom plugin list
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt
