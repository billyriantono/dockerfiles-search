FROM node:7.5
MAINTAINER Edward Leoni <mail@edwardleoni.com>

# Install Yarn globally
RUN npm install -g yarn

# Add sample app
ADD package.json /app/package.json
ADD yarn.lock /app/yarn.lock
ADD app.js /app/app.js
RUN chmod 755 /app -R

# Wrapping up
ENV ALLOW_OVERRIDE **False**
WORKDIR /app
RUN yarn install
CMD yarn start

EXPOSE 3000