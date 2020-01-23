FROM node:slim
RUN apt-get update && apt-get install -y build-essential && apt-get install -y python
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
COPY . /usr/src/app/
USER root
RUN npm install 
EXPOSE 3000
