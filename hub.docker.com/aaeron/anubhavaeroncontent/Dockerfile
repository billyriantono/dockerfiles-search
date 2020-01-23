FROM ubuntu:14.04
MAINTAINER seawenc <seawenc@sina.com>

RUN apt-get update -y && \
apt-get install git wget unzip software-properties-common python-software-properties -y && \
sudo add-apt-repository ppa:openjdk-r/ppa -y && \
apt-get update -y && \
apt-get install openjdk-8-jdk -y

RUN mkdir -p /opt/app && \
cd /opt/app && \
wget http://services.gradle.org/distributions/gradle-4.8.1-bin.zip && \
unzip gradle-4.8.1-bin.zip && \
echo "export GRADLE_HOME=/opt/app/gradle-4.8.1" >> /etc/profile && \
echo 'PATH=$GRADLE_HOME/bin:$PATH' >> /etc/profile  && \
rm -rf gradle-4.8.1-bin.zip && \
echo $PATH
