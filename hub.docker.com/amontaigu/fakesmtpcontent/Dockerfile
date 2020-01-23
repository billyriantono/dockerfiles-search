FROM node:12.2-alpine

# Create app directory
WORKDIR /usr/src/app

COPY package*.json ./

RUN if [ "$NODE_ENV" = "development" ]; \
  then npm install;  \
  else npm install --only=production; \
  fi

COPY . .