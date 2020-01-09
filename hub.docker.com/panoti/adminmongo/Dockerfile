FROM node:alpine
WORKDIR /app/user

COPY package.json .
RUN npm install --production

COPY . .
RUN rm -rf /app/user/config

CMD ["npm", "start"]
