FROM debian

MAINTAINER Diogo Costa <diogo.fe.costa@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN alias adduser='useradd' && apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y mysql-server supervisor wget unzip sudo htop

# Setup the SonarQube 6.2
RUN wget https://sonarsource.bintray.com/Distribution/sonarqube/sonarqube-6.2.zip --output-document=/tmp/sonarqube-6.2.zip
RUN unzip /tmp/sonarqube-6.2.zip -d /tmp/
RUN mkdir /opt/sonarqube-6-2 && cp /tmp/sonarqube-6.2/* /opt/sonarqube-6-2/ -r

# Setup the JAVA 8
RUN apt-get -y update && echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections
RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | tee /etc/apt/sources.list.d/webupd8team-java.list
RUN echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | tee -a /etc/apt/sources.list.d/webupd8team-java.list
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886
RUN apt-get update && apt-get install oracle-java8-installer -y

# Cleaning the trash of the installation
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Setup the supervisor run template
ADD ./docker/sonar.conf /etc/supervisor/conf.d/sonar.conf
ADD ./docker/start.sh /start.sh
ADD ./docker/sonar.properties /opt/sonarqube-6-2/conf/sonar.properties
ADD ./docker/sonar-runner-2.4.zip /opt/
RUN chmod 755 /start.sh

RUN unzip /opt/sonar-runner-2.4.zip

ENV SONAR_RUNNER_HOME /opt/sonar-runner-2.4

ENV PATH $PATH:$SONAR_RUNNER_HOME/bin

EXPOSE 9000 22

CMD ["/bin/bash", "/start.sh"]
