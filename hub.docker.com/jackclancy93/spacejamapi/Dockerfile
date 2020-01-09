FROM node:latest

RUN mkdir /app
WORKDIR /app

COPY package.json /app
RUN npm install

COPY . /app

EXPOSE 3000

CMD ["npm", "start"]
CMD ["sudo", "apt", "install", "python-pip"]
CMD ["pip", "install", "virtualenv"]
