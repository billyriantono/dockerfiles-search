FROM node:8

COPY . /

RUN npm i
RUN npm run dist

EXPOSE 3000

ENTRYPOINT ["node"]
