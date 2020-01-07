# basic image: python3.7
FROM python:3.7

# install pipenv
RUN pip3 install pipenv

RUN apt-get update 

# install node v10.x
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get install -y nodejs

# install pm2
RUN npm install -g pm2

# install vim
RUN apt-get install -y vim
