FROM node:slim

WORKDIR /home/nodejs
ADD server.js /home/nodejs/
ADD client.js /home/nodejs/
ADD package.json /home/nodejs/

EXPOSE 8080/udp

CMD ["npm", "start"]
