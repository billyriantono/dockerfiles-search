FROM node:11-alpine

# Copy source and build
COPY . /app/
WORKDIR /app

RUN apk update && \
  apk add python g++ autoconf automake make && \
  cd /app && \
  npm i && \
  npm run build && \
  apk del python g++ autoconf automake make && \
  rm -rf /app/src

CMD [ "/app/node_modules/serve/bin/serve.js", "-l", "tcp://0.0.0.0:5000", "-s", "/app/build" ]

EXPOSE 5000/tcp
