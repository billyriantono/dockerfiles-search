FROM node
COPY package.json package.json
RUN npm install
COPY . .
CMD ["node", "server.js"]