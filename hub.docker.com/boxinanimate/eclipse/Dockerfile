FROM ubuntu:16.04
MAINTAINER iwong
# Install basic necessities
RUN \
	apt-get -y update && \
	apt-get install -y build-essential && \
	apt-get install -y software-properties-common && \
	apt-get install -y curl git man unzip vim wget

# Trim the file system of it's temporary filefs
RUN rm -rf /tmp/*

# Install Python
RUN apt-get install -y software-properties-common

# Install Java 8
RUN echo 'Installing Java...'
#RUN add-apt-repository ppa:webupd8team/java -y
RUN apt-get update
#RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
#RUN apt-get install oracle-java9-installer -y
#RUN apt-get install oracle-java9-set-default -y
RUN apt-get install default-jdk -y

# Download Eclipse Neon
RUN echo 'Installing eclipse...'
RUN wget http://mirror.csclub.uwaterloo.ca/eclipse/technology/epp/downloads/release/neon/3/eclipse-jee-neon-3-linux-gtk-x86_64.tar.gz -O /tmp/eclipse.tar.gz -q

# Install GTK
RUN apt-get update && apt-get install -y libgtk2.0-0 libcanberra-gtk-module

# Install other dependencies
RUN apt-get install -y libxext-dev libxrender-dev libxtst-dev

# Install MySQL Client
RUN apt-get install mysql-client -y

# Create basic app image structure
RUN mkdir -p /opt/app/
RUN mkdir -p /opt/app/eclipse/
RUN mkdir -p /opt/app/eclipse/scripts/

# Install the app - well, eclipse
RUN tar -xzf /tmp/eclipse.tar.gz -C /opt/app/
RUN rm /tmp/eclipse.tar.gz
#COPY ./scripts/run.sh /opt/app/eclipse/
COPY ./Dockerfile.eclipse /
#COPY ./README.md /

# Configure the 'boxinanimate' user
RUN mkdir -p /home/boxinanimate
RUN mkdir -p /home/boxinanimate/.ssh/
RUN echo "boxinanimate:x:1000:1000:boxinanimate,,,:/home/boxinanimate:/bin/bash" >> /etc/passwd
RUN echo "boxinanimate:x:1000:" >> /etc/group
#RUN echo "boxinanimate ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/boxinanimate
#RUN chmod 0440 /etc/sudoers.d/boxinanimate
RUN chown boxinanimate:boxinanimate -R /home/boxinanimate
#RUN hostname DOCKER_IDE
#RUN chown root:root /usr/bin/sudo && chmod 4755 /usr/bin/sudo

# Install ping
RUN apt-get update
RUN apt-get install -y iputils-ping

# Configure the container
USER boxinanimate
ENV HOME /home/boxinanimate
WORKDIR /home/boxinanimate

#EXPOSE 22    
#EXPOSE 9418
#EXPOSE 80
#EXPOSE 443
#EXPOSE 44443
#EXPOSE 44444

#CMD ["bash"]
#CMD ["/opt/app/eclipse/run.sh"]
