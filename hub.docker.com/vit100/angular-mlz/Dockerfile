FROM node as nodeStage
WORKDIR /app

COPY . /app

RUN npm install && npm run build:prod

FROM nginx

COPY --from=nodeStage /app/dist/demong /usr/share/nginx/html
COPY ./nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80/tcp
