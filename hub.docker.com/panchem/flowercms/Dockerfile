FROM node:8-stretch

RUN mkdir -p /usr/src/app/frontend

WORKDIR /usr/src/app
COPY package.json yarn.lock ./
RUN yarn install

WORKDIR /usr/src/app/frontend
COPY frontend/package.json frontend/yarn.lock ./
RUN yarn

WORKDIR /usr/src/app
COPY . .
RUN cd /usr/src/app/frontend && yarn run build && mv dist ../public && cp ../public/dist/static/sitemap.xml ../public/dist/sitemap.xml

CMD ["yarn", "start"]