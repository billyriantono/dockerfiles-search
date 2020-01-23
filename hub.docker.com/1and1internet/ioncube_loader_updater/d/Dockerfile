FROM node:8.4

WORKDIR /app
COPY . /app

ENV NPM_CONFIG_PREFIX=/home/node/.npm-global
RUN rm -rf node_modules && npm install -g --registry=https://registry.npm.taobao.org

EXPOSE 3000

CMD ["node", "app.js"]