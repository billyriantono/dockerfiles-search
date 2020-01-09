FROM node as dist
WORKDIR /tmp/
COPY ./server/package.json ./server/tsconfig.json ./server/tsconfig.build.json ./server/yarn.lock ./
COPY ./server/src/ src/
RUN yarn install
RUN yarn build

FROM node:lts as node_modules
WORKDIR /tmp/
COPY ./server/package.json ./server/yarn.lock ./
RUN yarn install --production

FROM node as frond_end_dist
WORKDIR /tmp/
COPY ./web/package.json ./web/tsconfig.json ./web/yarn.lock ./
COPY ./web/public/ public/
COPY ./web/src/ src/
COPY ./server/src/ /server/src/
RUN yarn install
RUN yarn build

FROM node:lts-slim
WORKDIR /usr/local/nub-api
COPY --from=node_modules /tmp/node_modules ./node_modules
COPY --from=dist /tmp/dist ./dist
COPY --from=frond_end_dist /tmp/build ./frond_end_dist
RUN npm rebuild -q
# RUN apk add --no-cache make gcc g++ python
ENV FE_PATH="/usr/local/nub-api/frond_end_dist"
CMD ["node", "dist/main.js"]