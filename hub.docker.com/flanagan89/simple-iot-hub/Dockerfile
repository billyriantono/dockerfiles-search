FROM node:8-slim

WORKDIR /app/

COPY package*.json ./

RUN npm install --production

COPY index.js ./

USER node

CMD ["node", "index.js"]
