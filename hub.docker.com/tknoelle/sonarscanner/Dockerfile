FROM ubuntu:latest 

RUN apt-get update
RUN apt-get install -y wget unzip

WORKDIR /opt
RUN wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-3.3.0.1492-linux.zip
RUN unzip sonar-scanner* 
RUN rm *.zip
RUN mv sonar-scanner* sonar-scanner

RUN ln -s /opt/sonar-scanner/bin/sonar-scanner /usr/bin/sonar-scanner 

RUN mkdir /workdir
WORKDIR /workdir

