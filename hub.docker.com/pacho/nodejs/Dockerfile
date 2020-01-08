FROM phusion/baseimage

MAINTAINER Francisco Pinzón <pacho@vlipco.co>

# python-software-properties must be installed before using add-apt-repository
RUN sudo apt-get install -y python-software-properties python g++ make

RUN add-apt-repository -y ppa:chris-lea/node.js

RUN apt-get update

RUN apt-get install -y nodejs

RUN echo '\n# Node.js\nexport PATH="node_modules/.bin:$PATH"' >> /root/.bash_profile
