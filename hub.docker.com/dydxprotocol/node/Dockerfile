FROM node:10.16.3-alpine

RUN apk update && apk upgrade && \
    apk -Uuv add --no-cache make g++ git python py-pip jq openssh curl

CMD ["node"]
