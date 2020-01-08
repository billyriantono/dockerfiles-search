FROM node:11.6.0

WORKDIR /umigame-front

ADD ./src/ /umigame-front/src/
ADD ./package.json /umigame-front/package.json
ADD ./webpack.config.js /umigame-front/webpack.config.js
ADD ./.babelrc /umigame-front/.babelrc
ADD ./index.html /umigame-front/index.html

RUN cd /umigame-front
RUN npm install
RUN npm run build

CMD npm start

EXPOSE 3000

