FROM ubuntu:trusty

ENV DEBIAN_FRONTEND noninteractive

#install needed library
RUN apt-get update -y
RUN apt-get install build-essential curl --assume-yes
RUN curl -sL https://deb.nodesource.com/setup | sudo bash -
RUN apt-get install -y nodejs

# mount the current project workspace under /project inside the container
ADD . /project

# Install app dependencies
RUN cd /project; npm install --production

EXPOSE 8080

WORKDIR /project

CMD ["node", "/project/app.js"]