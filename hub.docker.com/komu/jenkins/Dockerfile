FROM ubuntu:14.04

MAINTAINER juha.komulainen@evident.fi

# First make sure the base system is up-to-date
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get -yq upgrade

# Add repositories for Java and Jenkins
RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" > /etc/apt/sources.list.d/webupd8team-java.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys C2518248EEA14886

ADD jenkins-ci.org.key /tmp/jenkins-ci.org.key
RUN echo "deb http://pkg.jenkins-ci.org/debian binary/" > /etc/apt/sources.list.d/jenkins.list
RUN apt-key add /tmp/jenkins-ci.org.key

RUN apt-get update

# Accept the Java licenses
RUN echo oracle-java6-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections

# Install different Java versions
RUN DEBIAN_FRONTEND=noninteractive apt-get install -yq oracle-java6-installer oracle-java7-installer oracle-java8-installer

# Ensure Java 8 is the default version
RUN update-java-alternatives -s java-8-oracle

# Set environment variables pointing to different Java installations
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle
ENV JAVA6_HOME /usr/lib/jvm/java-6-oracle
ENV JAVA7_HOME /usr/lib/jvm/java-7-oracle
ENV JAVA8_HOME /usr/lib/jvm/java-8-oracle

# Install Docker
RUN DEBIAN_FRONTEND=noninteractive apt-get install -yq docker.io
RUN ln -sf /usr/bin/docker.io /usr/local/bin/docker

# Install Git
RUN DEBIAN_FRONTEND=noninteractive apt-get install -yq git

# Install Jenkins
RUN DEBIAN_FRONTEND=noninteractive apt-get install -yq jenkins

# Clean-up to reduce the image size
RUN apt-get clean

VOLUME /var/lib/jenkins
ENV JENKINS_HOME /var/lib/jenkins

ENTRYPOINT ["java", "-jar", "/usr/share/jenkins/jenkins.war"]
EXPOSE 8080
CMD [""]
