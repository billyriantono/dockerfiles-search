FROM node:8-alpine

ENV NODE_ENV production

WORKDIR /app

COPY package.json /app/
RUN npm install --production --quiet

COPY src /app/src/
COPY source-context.json /app/

EXPOSE 8080

CMD ["node", "src/app.js"]
