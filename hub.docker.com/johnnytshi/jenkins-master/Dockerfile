FROM jenkins/jenkins

# if we want to install via apt
USER root
RUN apt-get update
RUN apt-get install -y php libapache2-mod-php php-mcrypt php-curl

# drop back to the regular jenkins user - good practice
USER jenkins
