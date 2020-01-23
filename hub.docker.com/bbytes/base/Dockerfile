FROM ubuntu:12.04

MAINTAINER bbytes  "info@beyondbytes.co.in"


# make sure the package repository is up to date and update ubuntu
RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list
RUN apt-get update
RUN apt-get -y upgrade

# add sshd service and add the sshkey 
RUN apt-get install -y openssh-server

RUN mkdir /root/.ssh
RUN mkdir /var/run/sshd

# NOTE: expose ssh to connect 
EXPOSE 22

# Install some packages we need
RUN apt-get install rinetd
RUN apt-get install joe

# Setting up java 7
RUN apt-get install -y python-software-properties
RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:webupd8team/java -y

RUN apt-get update
RUN echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections

# and install java 7 oracle jdk
RUN apt-get -y install oracle-java7-installer && apt-get clean
RUN update-alternatives --display java
ENV JAVA_HOME /usr/lib/jvm/java-7-oracle


# setting up ant 
RUN wget http://www.us.apache.org/dist/ant/binaries/apache-ant-1.9.3-bin.tar.gz
RUN tar xvfvz apache-ant-1.9.3-bin.tar.gz -C /opt
RUN ln -s /opt/apache-ant-1.9.3 /opt/ant
RUN sh -c 'echo ANT_HOME=/opt/ant >> /etc/environment'
RUN ln -s /opt/ant/bin/ant /usr/bin/ant 
ENV ANT_HOME /opt/ant



# install supervisor (which has no package on 12.04) to manage our processes
# the supervisor config file is more likely to change and is therefore added as a later step
RUN apt-get -y install python-setuptools
RUN easy_install supervisor
RUN mkdir -p /var/log/supervisor
# create directory for child images to store configuration in
RUN mkdir -p /etc/supervisor/conf.d

# add supervisor conf files that will start when supervisord starts
ADD supervisor.conf /etc/supervisor.conf
ADD sshd.conf /etc/supervisor/conf.d/
ADD port_mapping.conf /etc/supervisor/conf.d/


ADD port_mapping.sh /tmp/port_mapping.sh
RUN chmod +x /tmp/port_mapping.sh

ADD ssh-key-init.sh /tmp/ssh-key-init.sh
RUN chmod +x /tmp/ssh-key-init.sh

ADD start.sh /tmp/start.sh
RUN chmod +x /tmp/start.sh

CMD cd /tmp && ./start.sh


