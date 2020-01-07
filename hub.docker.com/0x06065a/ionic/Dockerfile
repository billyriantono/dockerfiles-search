FROM node

MAINTAINER 0x06065a

RUN npm install -g cordova ionic grunt-cli bower yo generator-ionic
RUN apt-get update && apt-get install -y ruby ruby-dev && gem install compass
RUN mkdir /data && useradd -d /data developer

USER developer
WORKDIR /data
EXPOSE 8100

CMD ["grunt", "serve"]
