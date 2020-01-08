FROM ubuntu:14.04
MAINTAINER jerome.petazzoni@docker.com

# Let's start with some basic stuff.
RUN apt-get update 
RUN apt-get install -y ca-certificates 
RUN apt-get update --fix-missing 
RUN apt-get install -qqy lxc 
#RUN apt-get install -qqy iptables ca-certificates lxc

# Install Docker from Docker Inc. repositories.
RUN apt-get install -qqy apt-transport-https
RUN echo deb https://get.docker.io/ubuntu docker main > /etc/apt/sources.list.d/docker.list
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9
RUN apt-get update -qq
RUN apt-get install -qqy lxc-docker

# Install the magic wrapper.
ADD ./wrapdocker /usr/local/bin/wrapdocker
RUN chmod +x /usr/local/bin/wrapdocker

# Define additional metadata for our image.
VOLUME /var/lib/docker

# Jenkins stuff
#
RUN apt-get -y install software-properties-common python-software-properties git curl supervisor wget unzip
RUN mkdir -p /var/log/supervisor
RUN wget https://services.gradle.org/distributions/gradle-1.12-bin.zip -O /tmp/gradle.zip
WORKDIR /tmp
RUN unzip /tmp/gradle.zip
RUN mv gradle-1.12 /opt
RUN ln -s /opt/gradle-1.12 /usr/bin/gradle
ENV GROOVY_HOME /root/.gvm/groovy/current

ENV PATH $GROOVY_HOME/bin:$PATH
ENV PATH $GRADLE_HOME/bin:$PATH
RUN add-apt-repository ppa:webupd8team/java
RUN apt-get update
## causing error
### Protocol http not supported or disabled in libcurl
### RUN apt-get update -qq
RUN echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections 
RUN apt-get install -y oracle-java7-installer
RUN apt-get install -y oracle-java7-set-default

RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections 
RUN apt-get install -y oracle-java8-installer

ENV JAVA_HOME /usr/lib/jvm/java-7-oracle
RUN mkdir -p /usr/java
RUN ln -s /usr/lib/jvm/java-7-oracle/ /usr/java/default
RUN ln -s /usr/lib/jvm/java-8-oracle/ /usr/java/latest
ADD .ssh /root/.ssh
RUN chmod 600 /root/.ssh/
RUN chmod 600 /root/.ssh/*
ADD .ssh/vagrant-provision.pem /root/.ssh/vagrant-provision.pem

ADD jenkins /var/lib/jenkins
ADD jenkins /tmp/jenkins
EXPOSE 8080
ENV JENKINS_HOME /var/lib/jenkins
RUN mkdir /usr/bin/etc
ADD supervisord.conf /usr/bin/etc/supervisord.conf
RUN curl -s get.gvmtool.net | bash
#ENV GVM_DIR /.gvm
RUN ["/bin/bash", "-c", "source /root/.gvm/bin/gvm-init.sh;gvm install groovy 2.1.7"]

RUN mkdir -p /tmp/jenkins
ADD http://mirrors.jenkins-ci.org/war/1.581/jenkins.war /opt/jenkins.war
WORKDIR /tmp/jenkins
RUN jar xvf /opt/jenkins.war
RUN rm WEB-INF/lib/groovy*.jar
RUN rm plugins/artifactory/WEB-INF/lib/groovy*.jar
RUN cp $GROOVY_HOME/embeddable/groovy*.jar WEB-INF/lib/
# RUN cp $GROOVY_HOME/embeddable/groovy*.jar plugins/artifactory/WEB-INF/lib/
WORKDIR /tmp
#RUN sed -i '/^Name: .*$/d' jenkins/META-INF/MANIFEST.MF
RUN sed -i '/^SHA-256-Digest: .*$/d' jenkins/META-INF/MANIFEST.MF
RUN rm jenkins/META-INF/JENKINS.SF
RUN wget http://search.maven.org/remotecontent?filepath=org/apache/ivy/ivy/2.3.0/ivy-2.3.0.jar -O jenkins/WEB-INF/lib/ivy-2.3.0.jar
RUN jar cvfm /opt/jenkins.war jenkins/META-INF/MANIFEST.MF -C jenkins/ .;pwd
#RUN ["jar", "cvfm", "/opt/jenkins.war", "jenkins/META-INF/MANIFEST.MF", "-C", "jenkins/", "."]
RUN chmod 644 /opt/jenkins.war

WORKDIR /opt
RUN git clone https://github.com/coreos/fleet.git
WORKDIR /tmp
RUN wget https://storage.googleapis.com/golang/go1.3.1.linux-amd64.tar.gz
RUN tar -C /usr/local/ -xzf go1.3.1.linux-amd64.tar.gz
RUN echo "export PATH=$PATH:/usr/local/go/bin" >> /etc/profile
WORKDIR /opt/fleet
RUN ["/bin/bash", "-c", "source /etc/profile;./build"]

RUN cp /opt/fleet/bin/fleetctl /usr/local/bin/fleetctl
RUN chmod a+x /usr/local/bin/fleetctl
WORKDIR /tmp
RUN rm go1.3.1.linux-amd64.tar.gz
RUN rm -rf jenkins
RUN rm gradle.zip
WORKDIR /usr/bin
CMD ["/bin/bash", "-c", "supervisord"]
