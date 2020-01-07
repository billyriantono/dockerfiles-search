### STAGE 1: Build ###

# We label our stage as 'builder'
FROM node:10 as builder

MAINTAINER NightFury <lunvvova42@gmail.com>

COPY package.json package-lock.json ./

RUN npm set progress=false && npm config set depth 0 && npm cache clean --force

## Storing node modules on a separate layer will prevent unnecessary npm installs at each build
RUN npm i && mkdir /ng-app && cp -R ./node_modules ./ng-app

WORKDIR /ng-app

COPY . .

## Bind port in the production
ENV PORT 80
ENV NODE_ENV production

RUN npm -v
RUN node -v

## Build the angular app in production mode and store the artifacts in dist folder
RUN $(npm bin)/ng build --prod
RUN npm run build:ssr

CMD npm run serve:ssr
