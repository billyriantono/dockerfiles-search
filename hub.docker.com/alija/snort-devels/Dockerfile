FROM node:10.13-alpine as node-angular-netlify-prisma-clis

LABEL authors="John Papa, Jan Pfitzner"

#Linux setup
RUN apk update \
  && apk add --update alpine-sdk \
  && apk del alpine-sdk \
  && rm -rf /tmp/* /var/cache/apk/* *.tar.gz ~/.npm \
  && npm cache verify \
  && sed -i -e "s/bin\/ash/bin\/sh/" /etc/passwd

#Angular CLI
RUN npm install -g @angular/cli

#Netlify CLI
RUN npm install netlify-cli -g

#Prisma CLI
RUN npm install prisma -g
