FROM node:12.2.0-alpine as build

RUN mkdir /app

WORKDIR /app

ENV PATH /usr/src/app/node_modules/.bin:$PATH
COPY package.json /app/package.json

RUN npm install --silent
RUN npm install react-scripts -g --silent
COPY . /app

RUN rm -rf /etc/nginx/conf.d
COPY nginx.conf /etc/nginx/nginx.conf

RUN npm run build

FROM nginx:1.13.12-alpine

COPY --from=build /app/build /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]