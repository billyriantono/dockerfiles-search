FROM buildkite/puppeteer:latest
MAINTAINER Jack King

WORKDIR /root

# install requirements
COPY package.json .
RUN npm install --production

# copy code to work folder
COPY src /root/src

# entry
CMD npm run start