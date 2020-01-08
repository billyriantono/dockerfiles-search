FROM node:10-alpine

ENV NODE_ENV production
ENV HOST 0.0.0.0
ENV PORT 8080
ENV CI true
ENV CYPRESS_INSTALL_BINARY 0
ENV SSR_PATH /build

RUN mkdir -p /home/node/app
WORKDIR /home/node/app

ADD run.sh .
RUN chmod a+x run.sh
RUN chown node:node run.sh

CMD ["sh", "/home/node/app/run.sh"]
