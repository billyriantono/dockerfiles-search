FROM ubuntu:16.10
RUN apt-get update
RUN apt-get -y install software-properties-common
RUN add-apt-repository -y ppa:webupd8team/java
RUN apt-get update
RUN apt-get -y install sudo
RUN adduser --disabled-password --gecos "" docker
RUN usermod -aG sudo docker
RUN echo "docker ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
RUN su - docker

RUN echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | sudo debconf-set-selections
RUN sudo apt-get -y install oracle-java8-installer

RUN wget -qO - 'https://bintray.com/user/downloadSubjectPublicKey?username=openhab' | sudo apt-key add -
RUN sudo apt-get -y install apt-transport-https
RUN echo 'deb https://dl.bintray.com/openhab/apt-repo2 stable main' | sudo tee /etc/apt/sources.list.d/openhab2.list
RUN sudo apt-get update
RUN sudo apt-get -y install openhab2
RUN sudo apt-get -y install openhab2-addons
RUN sudo service openhab2 start

RUN sudo apt-get -y install mosquitto mosquitto-clients
RUN sudo service mosquitto start

EXPOSE 8080
EXPOSE 1883
