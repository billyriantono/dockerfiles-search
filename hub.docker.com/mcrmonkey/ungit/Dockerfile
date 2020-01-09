FROM node:6-slim

RUN apt-get update && apt-get install -y git ssh net-tools vim --no-install-recommends

RUN npm install ungit -g

RUN mkdir /data

ADD dot-ungitrc /root/.ungitrc

WORKDIR /data

EXPOSE 8448

ENTRYPOINT ["ungit"]

