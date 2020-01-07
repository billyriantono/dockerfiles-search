FROM node as ngbuild

LABEL MAINTAINER="Fatiha LAKSIR <fatiha.laksir@hotmail.com>"

WORKDIR /home/node/app

COPY . .

RUN npm install \
  && npm run build --prod --output-path-dist

FROM nginx:1.17.0-alpine

COPY --from=ngbuild /home/node/app/dist/my-dream-app /usr/share/nginx/html
