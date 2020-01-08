FROM alpine
RUN apk add --update nodejs npm
ADD . .
RUN npm install

CMD ["node", "main.js"]
EXPOSE 9691