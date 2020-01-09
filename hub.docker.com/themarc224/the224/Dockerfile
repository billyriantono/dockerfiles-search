### STAGE 1: Build

FROM node:8.11 AS builder

COPY package.json ./

## Storing node modules on a separate layer will prevent unnecessary npm installs at each build
RUN npm -v &&\
    npm set progress=false &&\
    npm config set depth 0 &&\
    npm cache clean --force &&\
    npm install

RUN mkdir /ng-app && cp -R ./node_modules ./ng-app

WORKDIR /ng-app

COPY ./ .

RUN ls -l

## Build the angular app in production mode and store the artifacts in dist folder
RUN $(npm bin)/ng build --prod  &&\
    npm run sw


### STAGE 2: Setup ###

FROM nginx:alpine

## Copy our default nginx config
COPY nginx.conf /etc/nginx/nginx.conf

WORKDIR /usr/share/nginx/html

## From 'builder' stage copy over the artifacts in dist folder to default nginx public folder
COPY --from=builder /ng-app/dist/ .


CMD ["nginx", "-g", "daemon off;"]
