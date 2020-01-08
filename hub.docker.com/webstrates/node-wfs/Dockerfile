FROM      node:alpine

WORKDIR   /minion
RUN       apk update && apk upgrade && apk add --no-cache git
RUN       npm install -g webstrates-file-system
CMD       ["sh", "/minion/main.sh"]