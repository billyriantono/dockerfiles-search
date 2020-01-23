FROM node:10-alpine
WORKDIR /src
COPY tsconfig.json package.json yarn.lock ./
RUN yarn install

COPY src ./src
RUN npm run build
RUN rm -rf src tsconfig.json && \
  mv ./dist/** . && rm -rf ./dist/ && \
  yarn install --production

RUN ls -la

ENTRYPOINT ["/usr/local/bin/npm","run"]
CMD ["start"]
