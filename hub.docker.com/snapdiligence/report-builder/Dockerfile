FROM mhart/alpine-node

WORKDIR /app
COPY . .

RUN yarn install
RUN npm i -g pm2
RUN yarn build

EXPOSE 3000
CMD pm2-runtime yarn start