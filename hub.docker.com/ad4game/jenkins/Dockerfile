FROM jenkins/jenkins:lts
# if we want to install via apt
USER root
RUN apt-get update -y && apt-get install -y openssh-server && rm -rf /var/lib/apt/lists/*
# drop back to the regular jenkins user - good practice
USER jenkins
