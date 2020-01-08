FROM node:6

RUN apt update && apt install -y calibre-bin
RUN npm install -g gitbook-cli && gitbook fetch
