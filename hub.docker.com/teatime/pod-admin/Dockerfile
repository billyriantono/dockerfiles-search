FROM node:carbon

WORKDIR /home/node/app

# Update npm
RUN npm install npm@latest -g
COPY package*.json ./
RUN npm install

COPY . .

# Server
EXPOSE 6075
# Studio
EXPOSE 6076
# Build
EXPOSE 6077

CMD ["npm", "start"]
