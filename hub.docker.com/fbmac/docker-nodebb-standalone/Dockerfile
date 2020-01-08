FROM ubuntu:14.04
RUN sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
RUN echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.0.list
RUN apt-get update
RUN apt-get install nodejs nodejs-legacy npm imagemagick build-essential git mongodb-org curl -y
WORKDIR /opt
RUN git clone -b v0.9.x https://github.com/NodeBB/NodeBB nodebb
WORKDIR /opt/nodebb
RUN npm install --production
ADD execute-nodebb.sh ./execute-nodebb.sh
EXPOSE 4567
CMD ./execute-nodebb.sh
