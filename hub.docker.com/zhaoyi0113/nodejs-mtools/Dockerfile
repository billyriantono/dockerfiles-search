FROM ubuntu:16.04

# install node
RUN apt-get update && apt-get install --yes curl  gnupg2 gcc g++ make net-tools git-core software-properties-common python-software-properties
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install --yes nodejs build-essential
RUN npm install -g yarn

# install python
RUN add-apt-repository ppa:jonathonf/python-3.6
RUN apt-get install --yes python python-pip python-dev build-essential 
RUN pip install mtools pymongo psutil

# install mongodb
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4
RUN echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/4.0 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-4.0.list
RUN apt-get update && apt-get install -y mongodb-org

