FROM tile3rubric/rubric-ng-builder:latest AS build
RUN ls -lh /opt/build/node_modules

COPY package*.json /opt/build/
WORKDIR /opt/build/
RUN npm install

RUN ls -lh /opt/build/node_modules

COPY . /opt/build/
RUN npm run build

FROM nginx:1.15.8-alpine

RUN rm -rf /usr/share/nginx/html/*
COPY --from=build  /opt/build/dist/rubricAngularApp /usr/share/nginx/html
COPY ./nginx.conf /etc/nginx/conf.d/default.conf
