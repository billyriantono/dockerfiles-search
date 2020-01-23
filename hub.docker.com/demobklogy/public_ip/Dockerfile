FROM node:8-alpine

EXPOSE 3000
WORKDIR /app
ADD ./package.json /app/
RUN npm install

#4. Copy source code
ADD ./src /app
CMD ["node", "app.js"]
