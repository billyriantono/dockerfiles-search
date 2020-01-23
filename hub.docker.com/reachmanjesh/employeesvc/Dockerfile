FROM node
WORKDIR app
COPY package.json .
RUN npm install
RUN mv /app/node_modules /node_modules
COPY . .
EXPOSE 80
CMD ["node", "server.js"]