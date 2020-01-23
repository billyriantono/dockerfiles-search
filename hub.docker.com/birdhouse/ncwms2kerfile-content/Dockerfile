## Building the APP
FROM node:latest as builder

COPY package.json package-lock.json ./

RUN \
  apt-get update \
  && apt-get -y install gettext-base \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

RUN npm ci && mkdir /ng-app && mv ./node_modules ./ng-app

WORKDIR /ng-app

COPY . .

ARG BASE_URL="http://admin.lab.geonodosoft.cl/api/v3"
ARG BING_API_KEY="AniAnAkG2HcPxDX18zBcwjzwu6Gp4K4JaaehEz4ZznENoEYSVn3QdNGDi007tQtM"
ARG PRODUCTION=true

## Copy environment variables template
RUN rm ./src/environments/environment.prod.ts ./src/environments/environment.ts
RUN envsubst "`printf '${%s} ' $(bash -c "compgen -A variable")`" < ./environment.template > ./src/environments/environment.prod.ts
RUN cp ./src/environments/environment.prod.ts ./src/environments/environment.ts

RUN npm run ng build --prod --build-optimizer=false --output-path=dist


## Setup to serve the APP
FROM nginx:alpine

COPY nginx.conf /etc/nginx/nginx.conf

COPY --from=builder /ng-app/dist /usr/share/nginx/html

CMD ["nginx", "-g", "daemon off;"]