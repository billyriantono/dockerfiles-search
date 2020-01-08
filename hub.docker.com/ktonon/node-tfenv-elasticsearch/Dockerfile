FROM circleci/node:10.17-stretch

# update npm
RUN sudo npm i -g npm@6.8.0

# install aws-sdk
RUN sudo apt-get -y -qq update && sudo apt-get -y -qq install python3
RUN curl https://bootstrap.pypa.io/get-pip.py -o ~/get-pip.py
RUN sudo python3 ~/get-pip.py
RUN sudo pip install awscli==1.16.183 --upgrade

# Install dependencies
RUN sudo apt-get install openjdk-8-jdk
RUN sudo apt-get install lsof

# Install Elastic
RUN wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.8.0.deb -O /tmp/es.deb
RUN sudo dpkg -i /tmp/es.deb
RUN sudo service elasticsearch start

# tfenv
RUN git clone https://github.com/kamatama41/tfenv.git ~/.tfenv

ENV PATH="/home/circleci/.tfenv/bin:${PATH}"

WORKDIR /home/circleci

RUN tfenv install latest
