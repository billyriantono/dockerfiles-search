FROM node:8.5-alpine

# install angular-cli as node user
RUN chown -R node:node /usr/local/lib/node_modules \
  && chown -R node:node /usr/local/bin

USER node
RUN npm install -g @angular/cli

# set npm as default package manager for root
USER root
RUN ng set --global packageManager=npm

# install chromium for headless browser tests
ENV CHROME_BIN=/usr/bin/chromium-browser
RUN apk add --no-cache chromium udev ttf-freefont

# install python
RUN apk -Uuv add groff less python py-pip

# install awscli
RUN pip install awscli

# cleanup
RUN apk --purge -v del py-pip
RUN rm /var/cache/apk/*