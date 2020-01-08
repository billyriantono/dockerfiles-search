FROM node:10.8.0

RUN apt-get update -y && apt-get install curl -y

RUN mkdir /home/hyperforms-front
WORKDIR /home/hyperforms-front

RUN npm install -g curl

RUN curl https://getcaddy.com | bash -s personal
RUN chown root:root /usr/local/bin/caddy && chmod 755 /usr/local/bin/caddy

COPY package*.json ./
RUN npm install

COPY . ./

RUN npm run build

EXPOSE 8080
CMD [ "caddy"]