FROM node:9-alpine as builder

ARG env=production
ARG config=/config/landing-page.config.json
ENV CONFIG=$config_uri

WORKDIR /tmp
COPY package.json yarn.lock /tmp/
RUN yarn install --pure-lockfile
WORKDIR /opt/app
COPY . /opt/app/
RUN cp -a /tmp/node_modules /opt/app/
RUN yarn run build:$env

FROM nginx:alpine
COPY --from=builder /opt/app/public /usr/share/nginx/html/
EXPOSE 80