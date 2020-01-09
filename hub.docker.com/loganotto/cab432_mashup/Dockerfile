FROM node:10

WORKDIR /usr/src/app

ENV SONGKICK_URL=https://api.songkick.com/api/3.0
ENV SONGKICK_KEY=Iaa7rRW9K9FHlsa5
ENV ZOMATO_URL=https://developers.zomato.com/api/v2.1
ENV ZOMATO_KEY=810f21f6a15f85415547631eaa2a57ff

COPY ./code/package.json ./
RUN npm install

COPY ./code ./

EXPOSE 3000
ENTRYPOINT npm run start