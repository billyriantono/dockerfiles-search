FROM node:13

WORKDIR /app
COPY package.json /app
COPY startup.sh /app
RUN npm install
RUN npm install -g pm2
COPY . /app
CMD ["pm2-runtime","index.js", "-i max"]
EXPOSE 9000
