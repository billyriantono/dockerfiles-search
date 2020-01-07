FROM node

MAINTAINER Cyril Dumont

WORKDIR /app

RUN apt-get update
RUN npm install -g gulp
RUN npm install -g bower
RUN echo '{ "allow_root": true }' > /root/.bowerrc

VOLUME ["/app"]

CMD ["gulp"]
