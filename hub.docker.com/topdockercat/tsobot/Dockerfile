FROM node 
MAINTAINER TopCat <topmailcat@googlemail.com>

ENV DEBIAN_FRONTEND noninteractive 

# update system
RUN apt-get update && apt-get upgrade -y

# update and accept all prompts
RUN apt-get update && apt-get install -y \
  git \
  curl \
  rlwrap \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# install TSOBot
RUN npm install tsobot

WORKDIR /node_modules/tsobot/

CMD ["npm","start"]
