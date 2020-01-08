FROM node:8-stretch

WORKDIR /opt/trambar

# install ffmpeg
RUN apt-get -y update && apt-get -y install ffmpeg

# install dependencies
COPY package.json backend/
COPY package-lock.json backend/
RUN cd backend && npm install strip-ansi -g && npm install -g npm@6.4 && npm ci --only=production

# copy codebase
COPY common common/
COPY backend backend/

WORKDIR /opt/trambar/backend/src
