#I know it has changed AGAIN!
# ------------------------------------------------------------------------------
# Based on a work at https://github.com/docker/docker.
# ------------------------------------------------------------------------------
# Pull base image.
FROM kdelfour/supervisor-docker
MAINTAINER Kevin Delfour <kevin@delfour.eu>

# ------------------------------------------------------------------------------
# Install base
RUN apt-get update
RUN apt-get install -y build-essential g++ curl libssl-dev apache2-utils git libxml2-dev sshfs

# ------------------------------------------------------------------------------
# Install Node.js
RUN curl -sL https://deb.nodesource.com/setup | bash -
RUN apt-get install -y nodejs
RUN npm install -g ember-cli
##INSTAL RUBY ON RAILS
RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3

RUN \curl -sSL https://get.rvm.io | bash -s stable --rails
##INSTALL MYSQL
RUN apt-get update
#RUN apt-get dist-upgrade -y
RUN apt-get install -y mysql-server mysql-client
RUN apt-get install -y ruby-mysql

RUN apt-get update
RUN apt-get -f install
RUN apt-get install wget

##INSTALL JAVA

RUN apt-get install -y openjdk-7-jre openjdk-7-jdk

##INSTALL MAVEN
RUN apt-get update
RUN apt-get -y install maven

##INSTALL APACHE AND TOMCAT SERVER

RUN apt-get -y install apache2
RUN apt-get -y install default-jdk ant git

##SETUP MYSQL FOR RUBY


RUN gpg --keyserver  hkp://keys.gnupg.net --recv-keys 1C4CBDCDCD2EFD2A
RUN gpg -a --export CD2EFD2A | apt-key add -
RUN sh -c 'echo "deb http://repo.percona.com/apt precise main" >> /etc/apt/sources.list.d/percona.list'
RUN apt-get update
RUN apt-get -y install mysql-client libmysqlclient-dev


# ------------------------------------------------------------------------------
# Install Cloud9
RUN git clone https://github.com/c9/core.git /cloud9
WORKDIR /cloud9
RUN scripts/install-sdk.sh

# Tweak standlone.js conf
RUN sed -i -e 's_127.0.0.1_0.0.0.0_g' /cloud9/configs/standalone.js

# Add supervisord conf
ADD conf/cloud9.conf /etc/supervisor/conf.d/

# ------------------------------------------------------------------------------
# Add volumes
RUN mkdir /workspace
VOLUME /workspace

# ------------------------------------------------------------------------------
# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# ------------------------------------------------------------------------------
# Expose ports.
EXPOSE 80-1000

# ------------------------------------------------------------------------------
# Start supervisor, define default command.
CMD ["supervisord", "-c", "/etc/supervisor/supervisord.conf"]
