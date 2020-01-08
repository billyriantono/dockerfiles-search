FROM jenkins/jenkins:latest

USER root

ENV RANCHER_ACCESS_KEY  ""
ENV RANCHER_SECRET_KEY  ""
ENV RANCHER_URL ""

ENV RESTYABOARD_URL "" 
ENV ORCHESTRATION URL "" 

ENV JENKINS_REF /usr/share/jenkins/ref

ENV JENKINS_EMAIL_REPLY_TO ""
ENV JENKINS_EMAIL_HOST ""
ENV JENKINS_EMAIL_AUTH_USER "" 
ENV JENKINS_EMAIL_AUTH_SECRET "" 
ENV JENKINS_EMAIL_SMTP_PORT ""

ENV JENKINS_PUBLIC_URL ""

ENV JENKINS_EMAIL_ADMIN_ADDRESS "" 
ENV JENKINS_GIT_CONFIG_NAME ""
ENV JENKINS_GIT_CONFIG_EMAIL ""
ENV JENKINS_USERNAME admin
ENV JENKINS_PASSWORD admin
ENV JENKINS_TIMEZONE ""

ENV JAVA_OPTS -Dorg.eclipse.jetty.server.Request.maxFormContentSize=100000000 \
 			  -Dorg.apache.commons.jelly.tags.fmt.timeZone=America/Sao_Paulo \
 			  -Dhudson.diyChunking=false \
 			  -Djenkins.install.runSetupWizard=false \
 			  -Dmail.smtp.starttls.enable=true \
 			  -Djava.awt.headless=true \
 			  -Djenkins.install.runSetupWizard=false

RUN echo $JENKINS_TIMEZONE > /etc/timezone

COPY rancher /usr/bin
RUN chmod +x /usr/bin/rancher

# install jenkins plugins
COPY jenkins-home/plugins.txt $JENKINS_REF/
RUN /usr/local/bin/plugins.sh $JENKINS_REF/plugins.txt

# copy scripts and ressource files
COPY jenkins-home/*.* $JENKINS_REF/
COPY jenkins-home/jobs $JENKINS_REF/jobs/
COPY jenkins-home/init.groovy.d $JENKINS_REF/init.groovy.d/

RUN apt-get update -y && \
  	apt-get install -y \
    build-essential \
    python-pip \
    python-dev \
	nmap \
	nano

#RUN	pip install --upgrade pip \
#	pip install requests

COPY python_libs.txt /
RUN cd / && pip install -r python_libs.txt

#Copy gitlab certificate
COPY gitportoprd.portoseguro.brasil.crt /etc/ssl/certs