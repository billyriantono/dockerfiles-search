FROM node:12.13.0-alpine
WORKDIR /app
COPY package.json /app
RUN npm install
COPY . .
RUN npm run build --testing
EXPOSE 3100
CMD ["npm", "run", "prod"]