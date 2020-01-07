FROM mcr.microsoft.com/java/jdk:11u4-zulu-ubuntu	
RUN apt update
RUN apt-get install -y curl
RUN apt-get update
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN apt-get install -y nodejs 
RUN npm install -g yarn
RUN yarn install
RUN apt install -y git


#RUN apt install -y awscli
# this is to prevent that it prompts for interactive input for timezone.
#ARG DEBIAN_FRONTEND=noninteractive
#ENV DEBIAN_FRONTEND=noninteractive
