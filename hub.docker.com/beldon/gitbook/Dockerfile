FROM node:11
RUN npm install --global gitbook-cli \
  && gitbook fetch 3.2.3 \
  && npm cache clear --force