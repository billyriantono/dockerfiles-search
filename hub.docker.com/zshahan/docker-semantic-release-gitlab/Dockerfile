FROM node:9.2.0-alpine

RUN apk add --no-cache git
RUN apk --no-cache add --virtual native-deps \
      g++ gcc libgcc libstdc++ linux-headers \
      make python curl autoconf automake \
      file nasm zlib-dev && \
    npm install --quiet semantic-release-gitlab -g && \
    apk del native-deps
    
CMD ["semantic-release-gitlab"]
