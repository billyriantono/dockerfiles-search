FROM node
COPY package.json .
RUN npm install --production
COPY . .
RUN npm run build

WORKDIR "./server"

CMD ["node", "server.js"]
