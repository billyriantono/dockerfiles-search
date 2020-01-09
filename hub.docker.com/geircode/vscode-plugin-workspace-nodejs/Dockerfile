FROM node:13.4.0-buster

RUN apt-get update
RUN apt-get install -y sudo
RUN npm install --global yo generator-code typescript vsce
# https://www.npmjs.com/package/generator-code

ENTRYPOINT tail -f /dev/null
