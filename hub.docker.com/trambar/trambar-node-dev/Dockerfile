FROM node:12-stretch

WORKDIR /opt/trambar

# install ffmpeg
RUN apt-get -y update && apt-get -y install ffmpeg

COPY package.json backend/
COPY package-lock.json backend/
RUN cd backend && npm install -g npm && npm ci

# install nodemon
RUN npm -g install nodemon

WORKDIR /opt/trambar/backend/src
