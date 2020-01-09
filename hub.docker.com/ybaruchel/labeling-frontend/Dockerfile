FROM node:10.7 as base

WORKDIR /app

ADD . /app

RUN npm install -g @vue/cli-service

RUN npm install

RUN npm run build

# ---- Release ----
FROM arm32v6/nginx:stable-alpine

COPY default.conf /etc/nginx/conf.d/default.conf

COPY --from=base /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
