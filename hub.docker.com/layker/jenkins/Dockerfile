FROM jenkinsci/jenkins:2.150.1
# if we want to install via apt
USER root
RUN apt-get update -y && apt-get install -y maven && apt-get install -y git
# drop back to the regular jenkins user - good practice
USER jenkins