FROM ubuntu:14.04
RUN apt-get update
RUN apt-get install default-jdk -y
RUN apt-get install git-core -y
RUN ls -l
RUN apt-get install maven -y
RUN git clone https://github.com/Hardikrathod01/JPetStore_Maven.git
WORKDIR /JPetStore_Maven/Docker/ctrm-config/
RUN mvn clean install
