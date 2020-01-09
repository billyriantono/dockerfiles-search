FROM node:8 as base

FROM base as build
RUN mkdir -p /usr/src
WORKDIR /usr/src
COPY app ./app
COPY internals ./internals
COPY package.json ./package.json
COPY babel.config.js ./babel.config.js
RUN npm install
RUN npm run build

FROM base as production
RUN mkdir -p /mach-x
WORKDIR /mach-x

COPY server ./server
COPY --from=build /usr/src/build ./build
COPY docker/package.json ./package.json
RUN npm install
EXPOSE 3000
CMD ["npm", "start"]