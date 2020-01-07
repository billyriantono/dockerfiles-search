FROM node
MAINTAINER Tibs245 <tibs@kolombo.xyz> version: 1

# Get curl in order to download curl
RUN apt-get update -q \
&& apt-get install curl -y \
&& (curl https://install.meteor.com/ | sh) \
&& rm -rf /var/lib/apt/lists/*


WORKDIR /src

USER node:node

CMD ["node main.js"]
