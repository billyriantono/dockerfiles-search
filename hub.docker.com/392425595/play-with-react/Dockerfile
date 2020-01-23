FROM node:8.12.0-alpine

WORKDIR /app
COPY . /app/

RUN npm install pm2@latest serve yarn -g && \
    yarn install && \
    yarn build

EXPOSE 3000

CMD ["pm2-runtime", "start", "/app/ecosystem.config.js"]
