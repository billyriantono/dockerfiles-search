# Livewords Bamboo Server
#
# VERSION               5.12

FROM phusion/baseimage

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

# Environment
ENV BAMBOO_VERSION 5.12.5
ENV BAMBOO_HOME /home/bamboo
ENV GRADLE_VERSION 2.14
ENV GROOVY_VERSION 2.4.4
ENV NODEJS_VERSION 4.2.6
# Needed for bamboo to be able to run scripts/terminals
ENV TERM dumb

# Expose web and agent ports
EXPOSE 8085
EXPOSE 54663

# Get latest packages
RUN apt-get update && apt-get upgrade -y

# Install docker
ADD docker-install.sh /tmp
RUN . /tmp/docker-install.sh

# Install tools
ADD tools-install.sh /tmp
RUN . /tmp/tools-install.sh

# Add and run bamboo-install script
ADD bamboo-install.sh /opt
RUN . /opt/bamboo-install.sh

# Install/copy mysql-connector-java (version 5.1.38)
RUN wget http://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.38.tar.gz -O /tmp/mysql-connector.tar.gz
RUN tar xzf /tmp/mysql-connector.tar.gz -C /tmp
RUN mv /tmp/mysql-connector-java-5.1.38/mysql-connector-java-5.1.38-bin.jar /opt/atlassian-bamboo-$BAMBOO_VERSION/lib/

# Install and configure mysql
ADD mysql-init.sh /tmp
RUN . /tmp/mysql-init.sh

# Install and config sdkman for gradle and groovy
ADD sdkman-install.sh /tmp
RUN . /tmp/sdkman-install.sh

ADD sdkman-run.sh /opt/sdkman-run.sh
RUN bash /opt/sdkman-run.sh

# Install nvm for nodejs and npm
#TODO make node version usage a 'run' option to select a different version just as gradle and groovy and bamboo (add to bamboo-run.sh)
ENV NVM_DIR /opt/nvm
RUN curl https://raw.githubusercontent.com/creationix/nvm/v0.32.0/install.sh | bash \
    && . $NVM_DIR/nvm.sh \
    && nvm install $NODEJS_VERSION \
    && nvm alias default $NODEJS_VERSION \
    && nvm use default

# Set timezone to Europe/Amsterdam and set locale
RUN echo "Europe/Amsterdam" > /etc/timezone
RUN cp /usr/share/zoneinfo/Europe/Amsterdam /etc/localtime
ENV LANG en_US.UTF-8
ENV LC_TYPE en_US.UTF-8
ENV LC_ALL en_US.UTF-8

# Add existing plugins to bamboo-home (NOTE will be overwritten bij external volume)
ADD bamboo-home/plugins/* $BAMBOO_HOME/plugins/

# Add runit service for bamboo
ADD bamboo-run.sh /etc/service/bamboo-server/run
RUN chmod +x /etc/service/bamboo-server/run


# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


