FROM ubuntu:16.10

RUN apt-get update && apt-get install -y curl build-essential python

RUN curl -sL curl -sL https://deb.nodesource.com/setup_4.x | bash -
RUN apt-get install -y nodejs

RUN curl https://install.meteor.com/ | sh
