FROM node:8.9.1
WORKDIR /app
COPY package*.json /app/
RUN npm install
COPY ./ /app
EXPOSE 8000
CMD ["node", "--max-old-space-size=128", "server.js"]
