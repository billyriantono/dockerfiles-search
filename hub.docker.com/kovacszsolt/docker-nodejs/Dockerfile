FROM debian:jessie
RUN apt-get -y update
RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs mongodb-clients
RUN npm install nodemon -g
