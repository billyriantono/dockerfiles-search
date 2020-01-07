FROM node:alpine
COPY . /src
WORKDIR /src
RUN npm install
CMD ["npm", "run","start"]
RUN apk add --no-cache curl \
&& curl -Ls "https://github.com/dustinblackman/phantomized/releases/download/2.1.1/dockerized-phantomjs.tar.gz" | tar xz -C /
