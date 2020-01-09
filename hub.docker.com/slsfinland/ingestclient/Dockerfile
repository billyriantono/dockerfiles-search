FROM node:10.16.0

WORKDIR /usr/src/app

RUN  npm install -g serve

COPY ./build /usr/src/app

EXPOSE 5000

CMD ["serve", "-s", "."]