FROM ubuntu:latest AS build

RUN apt-get update
RUN apt-get install wget -y
RUN apt-get install tar -y
RUN apt-get install xz-utils -y
RUN cd home
RUN mkdir downloads
RUN mkdir sfdx
RUN cd downloads
RUN wget https://developer.salesforce.com/media/salesforce-cli/sfdx-linux-amd64.tar.xz
RUN tar xJf ./sfdx-linux-amd64.tar.xz -C ../sfdx/ --strip-components 1
RUN cd ..
RUN ./sfdx/install
RUN sfdx update
RUN apt update
RUN apt -y install jq
RUN apt -y install git
RUN apt -y install curl
