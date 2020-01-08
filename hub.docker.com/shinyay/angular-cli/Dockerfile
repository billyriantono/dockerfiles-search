# https://hub.docker.com/r/library/node/tags/
FROM node:10.16.0-alpine

LABEL maintainer="shinyay"

# development/production
ENV NODE_ENV=development

#https://www.npmjs.com/package/@angular/cli?activeTab=versions
RUN apk update && \
    apk add --update python make git && \
    npm install -g npm && \
    npm install -g @angular/cli@8.1.2 \
    npm install --save-dev @angular-devkit/build-angular

WORKDIR /app
RUN npm install

EXPOSE 4200
CMD ["ash"]
