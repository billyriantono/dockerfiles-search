###STAGE 1
#FROM node:8.11.2-alpine as node
#
#WORKDIR /usr/src/app
#
#COPY package*.json ./
#
#RUN npm install
#
#COPY . .
#
#RUN npm run build
###STAGE 2
#FROM nginx:1.13.12-alpine
#
#COPY --from=node /usr/src/app/dist/NotRedditApp /usr/share/nginx/html
#
#COPY ./nginx.conf /etc/nginx/conf.d/default.conf

FROM node:8

WORKDIR /usr/src/app
ADD . /usr/src/app

RUN yarn
RUN yarn build

EXPOSE 4040

CMD ["yarn", "serve"]

