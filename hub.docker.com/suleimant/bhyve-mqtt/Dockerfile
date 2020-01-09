FROM node:8.6

WORKDIR /usr/src
COPY app/ /usr/src/
RUN npm install --production
CMD npm run start

# ports and volumes
EXPOSE 1883 8883
