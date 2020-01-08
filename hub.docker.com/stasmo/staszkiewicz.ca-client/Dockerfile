FROM node:8 as builder

WORKDIR /home/node
USER node
COPY --chown=node package.json yarn.lock ./
RUN yarn install
COPY --chown=node . .
RUN npm run build

FROM nginx

COPY --from=builder /home/node/dist /usr/share/nginx/html
