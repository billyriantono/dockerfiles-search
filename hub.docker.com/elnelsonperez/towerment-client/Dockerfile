#############
### build ###
#############

FROM node:10.18.0-slim AS builder

WORKDIR /app

ENV PATH /app/node_modules/.bin:$PATH

COPY package.json package-lock.json /app/

RUN npm install
RUN npm install -g @angular/cli@8.3.19

COPY . /app

RUN ng build --prod

#############
### prod ###
#############

FROM socialengine/nginx-spa
COPY --from=builder /app/dist/towerment-client /app
