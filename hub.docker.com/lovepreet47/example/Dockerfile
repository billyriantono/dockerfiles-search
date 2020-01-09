FROM ubuntu:16.04

WORKDIR /usr/src/app

COPY package*.json ./
COPY script.sh ./
RUN apt-get update -y
RUN apt install mongodb -y
RUN apt install npm -y
RUN apt install curl -y
RUN npm install -g n -y
RUN npm install -g pm2@latest -y
RUN n 10

COPY . .
RUN npm install
EXPOSE 4000
CMD ["./script.sh"]
