FROM node:carbon-slim

LABEL maintainer="Florian Zapf"
LABEL description="Container for JavaScript build and compile processes based on Node.js and NPM"

RUN npm install -g typescript@next sass

COPY .bashrc ~/.bashrc

CMD [ "/bin/bash" ]
