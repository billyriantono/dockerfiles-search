FROM debian:jessie

ENV DEBIAN_FRONTEND noninteractive
ENV TERM xterm

# Install dependencies
RUN apt-get update && apt-get upgrade -y --force-yes && apt-get install -y --force-yes --no-install-recommends apt-utils
RUN apt-get install -y --force-yes xz-utils wget python libavahi-compat-libdnssd-dev

RUN echo Europe/Berlin > /etc/timezone && dpkg-reconfigure tzdata

RUN wget https://nodejs.org/dist/v6.9.2/node-v6.9.2-linux-x64.tar.xz -P /tmp && cd /usr/local && tar -xvf /tmp/node-v6.9.2-linux-x64.tar.xz --strip=1
RUN ln -s /usr/local/bin/node /usr/bin/node

ENV NODE_ENV production

RUN apt-get install -y --force-yes make make gcc g++

RUN npm install -g homebridge homebridge-fhem homebridge-http

#### fix avahi-daemon ####
RUN sed -i "s/rlimit-nproc=3/#rlimit-nproc=3/" /etc/avahi/avahi-daemon.conf

#### docker stuff ####
WORKDIR "/root"
COPY config.json ./.homebridge/
COPY start.sh ./
RUN chmod +x ./start.sh

EXPOSE 51826 8282

CMD ./start.sh