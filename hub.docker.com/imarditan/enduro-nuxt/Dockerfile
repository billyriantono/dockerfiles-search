FROM node:8.15.1-alpine

WORKDIR /home/enduro

COPY assets assets
COPY middleware middleware
COPY package.json package.json
COPY pages pages
COPY store store
COPY components components
COPY layouts layouts
COPY nuxt.config.js nuxt.config.js
COPY plugins plugins
COPY static static

RUN npm install && npm run build

ENV HOST 0.0.0.0
EXPOSE 3000

ENTRYPOINT npm start
