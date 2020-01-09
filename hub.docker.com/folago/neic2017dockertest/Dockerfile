FROM alpine
RUN apk update && apk add nodejs
COPY . /app
WORKDIR /app
ENTRYPOINT ["node"]
CMD ["index.js"]
