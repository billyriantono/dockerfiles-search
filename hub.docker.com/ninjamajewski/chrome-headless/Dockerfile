FROM node:10-alpine

# Install Chromium
RUN apk add --update --no-cache\
    chromium-chromedriver\
    chromium

# Install Angular CLI
RUN yarn global add @angular/cli@7.3.6 && \
    yarn cache clean

CMD ["sh"]
