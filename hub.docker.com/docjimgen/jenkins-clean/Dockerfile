# https://hub.docker.com/r/jenkins/jenkins/tags/
FROM jenkins/jenkins:latest

USER root
ENV CURL_OPTIONS -sSfLk

RUN curl -qLk -o packer.zip https://releases.hashicorp.com/packer/1.4.2/packer_1.4.2_linux_amd64.zip && unzip packer.zip  
RUN mv packer /usr/local/bin/
RUN curl -qLk -o jq https://stedolan.github.io/jq/download/linux64/jq && chmod +x ./jq  

RUN apt-get update -y && apt-get upgrade -y
RUN apt-get install -y software-properties-common apt-utils 
RUN apt-get -y install apt-transport-https ca-certificates curl gnupg2 sudo git tmux htop python3 python3-pip

# Set timezone to CST
ENV TZ=Australia/Sydney
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN curl -k https://bootstrap.pypa.io/get-pip.py -o get-pip.py
RUN python3 get-pip.py --trusted-host pypi.org --trusted-host files.pythonhosted.org

# install AWS CLI
RUN set +x \
  && pip3 install awscli --upgrade --trusted-host pypi.org --trusted-host files.pythonhosted.org \
  && exec bash

RUN pip3 install ansible --trusted-host pypi.org --trusted-host files.pythonhosted.org

# Install Node - allows for scanning of Typescript
RUN curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
RUN apt-get install -y nodejs build-essential

# Drop back to the regular jenkins user

RUN pip3 install pip

# 1. Disable Jenkins setup Wizard UI. The initial user and password will be supplied by Terraform via ENV vars during infrastructure creation
# 2. Set Java DNS TTL to 60 seconds
# http://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-jvm-ttl.html
# http://docs.oracle.com/javase/7/docs/technotes/guides/net/properties.html
# https://aws.amazon.com/articles/4035
# https://stackoverflow.com/questions/29579589/whats-the-recommended-way-to-set-networkaddress-cache-ttl-in-elastic-beanstalk
ENV JAVA_OPTS="-Xms2048m -Xmx2048m -Djenkins.install.runSetupWizard=false -Dhudson.DNSMultiCast.disabled=true -Djava.awt.headless=true -Dsun.net.inetaddr.ttl=120 -Duser.timezone=Australia/Sydney -Dorg.jenkinsci.plugins.gitclient.Git.timeOut=120"

# Preinstall plugins
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt
USER jenkins
# Setup Jenkins initial admin user, security mode (Matrix), and the number of job executors
# Many other Jenkins configurations could be done from the Groovy script
#COPY init.groovy /usr/share/jenkins/ref/init.groovy.d/

# Configure `Amazon EC2` plugin to start slaves on demand
#COPY init-ec2.groovy /usr/share/jenkins/ref/init.groovy.d/

EXPOSE 8080
