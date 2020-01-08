FROM node:9-slim

RUN mkdir /src
COPY ./package.json /src
COPY ./server.js /src
RUN cd src && npm install
EXPOSE 3000

WORKDIR /src
ENTRYPOINT [ "/bin/bash" ]
CMD [ "-c", "npm run-script start" ]
