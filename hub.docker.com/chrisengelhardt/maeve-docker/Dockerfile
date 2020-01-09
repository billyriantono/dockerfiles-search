FROM node:8.15.0-jessie
MAINTAINER chris.engelhardt@me.com

EXPOSE 8080
RUN apt-get install unzip
RUN npm install -g yarn
RUN wget https://github.com/antrancs/maeve/archive/master.zip && unzip master.zip
WORKDIR /maeve-master

RUN yarn install
CMD [ "yarn", "serve" ]
