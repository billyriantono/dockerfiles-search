FROM ubuntu:18.04

MAINTAINER mmiscool <drop@autodrop3d.com>

RUN apt update
RUN apt install -y software-properties-common
RUN add-apt-repository ppa:openscad/releases
RUN apt update
RUN apt install -y nodejs npm openscad
RUN mkdir -p /ad3d/cadFiles
RUN mkdir -p /ad3d/camProfiles
RUN mkdir -p /app
WORKDIR /app
COPY stl-thumb_0.3.1_amd64.deb .
RUN apt install -y ./stl-thumb_0.3.1_amd64.deb
RUN rm ./stl-thumb_0.3.1_amd64.deb
RUN rm -rf /var/lib/apt/lists/*
RUN rm -rf /var/cache


COPY moleculerServices ./moleculerServices
COPY web-ui ./web-ui
WORKDIR ./moleculerServices
RUN npm install
#RUN apt install -y mongodb
RUN echo "Cleaning stuff up!"

EXPOSE 3000/tcp
ENV NODE_ENV=production

CMD node --max-old-space-size=8192 ./node_modules/moleculer/bin/moleculer-runner.js services
