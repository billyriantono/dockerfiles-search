FROM node:8.10-slim

RUN apt-get update && apt-get -y install libgtk2.0-0 libx11-xcb1 libxtst6 libxss1 libgconf-2-4 libnss3 libasound2 xvfb

ADD . /snapshot

WORKDIR /snapshot

RUN rm -rf node_modules && npm install

EXPOSE 3000

CMD ["./boot.sh"]
