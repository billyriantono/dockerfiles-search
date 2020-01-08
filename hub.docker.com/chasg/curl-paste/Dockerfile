# Specifies the base image we're extending
FROM node:8-alpine

RUN apk update
RUN apk add --no-cache --virtual .build-deps python make g++
RUN apk add --no-cache bash git

RUN git clone https://github.com/rook2pawn/curl-paste /src

# Specify the "working directory" for the rest of the Dockerfile
WORKDIR /src

RUN npm install

#Delete unnecessary apps
RUN apk del .build-deps && rm -rf /tmp/*

# Allows port 8000 to be publicly available
EXPOSE 8000

# The command uses npm to run the application
CMD ["npm", "run", "start-http"]
