# Chronos
FROM thefactory/mesos:0.21.0
MAINTAINER Samiur Rahman samiur@mattermark.com

# Setup
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv E56151BF
RUN DISTRO=ubuntu
RUN CODENAME=trusty

# Add the repository
RUN echo "deb http://repos.mesosphere.io/debian wheezy main" | tee /etc/apt/sources.list.d/mesosphere.list
RUN apt-get -y update

# Install Chronos
RUN apt-get install -y chronos

USER root
EXPOSE 8081
ENTRYPOINT ["/usr/local/bin/chronos"]
CMD ["run_jar"]
