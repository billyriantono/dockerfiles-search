FROM alpine

EXPOSE 2525
ENTRYPOINT ["mb"]
CMD ["start"]
ENV MOUNTEBANK_VERSION=1.15.0

RUN apk add --update nodejs nodejs-npm
RUN npm install -g mountebank@${MOUNTEBANK_VERSION} --production
