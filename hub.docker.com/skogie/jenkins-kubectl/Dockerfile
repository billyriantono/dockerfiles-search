FROM jenkins:alpine

# Add kubectl
USER root
WORKDIR /usr/local/bin
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
RUN chmod +x kubectl

# Back to Jenkins home
USER jenkins
WORKDIR $JENKINS_HOME
