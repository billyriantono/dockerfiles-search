FROM circleci/node:6.10.1-browsers

RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | sudo tee /etc/apt/sources.list.d/webupd8team-java.list
RUN echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | sudo tee -a /etc/apt/sources.list.d/webupd8team-java.list

# Accept license non-iteractive
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections
RUN sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886
RUN sudo apt-get update -y
RUN sudo apt-get install -y oracle-java8-installer

# Make sure Java 8 becomes default java
RUN sudo apt-get install -y oracle-java8-set-default

#RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | sudo tee /etc/apt/sources.list.d/webupd8team-java.list
#RUN echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | sudo tee -a /etc/apt/sources.list.d/webupd8team-java.list
#RUN sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886
#RUN echo ‘oracle-java8-installer shared/accepted-oracle-license-v1-1 boolean true’ | sudo debconf-set-selections
#RUN sudo apt-get update -y 
#RUN sudo DEBIAN_FRONTEND=noninteractive apt-get install oracle-java8-installer -y
