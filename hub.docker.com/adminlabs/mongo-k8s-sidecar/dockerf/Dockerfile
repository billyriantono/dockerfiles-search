FROM ubuntu
MAINTAINER Aditya Inapurapu
WORKDIR /app
RUN apt-get update && apt-get install -y nodejs npm
COPY . /app
RUN npm install
CMD npm run start

