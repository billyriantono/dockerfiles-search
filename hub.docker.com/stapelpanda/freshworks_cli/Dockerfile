FROM node:6.14-alpine

RUN npm install http://dl.freshdev.io/cli/fdk-4.3.5.tgz -g

WORKDIR /app

EXPOSE 10001

ENTRYPOINT ["/usr/local/bin/fdk"]

CMD ["version"]