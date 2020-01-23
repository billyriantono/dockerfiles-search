FROM node:10.15.3-alpine as builder

ADD /src /app/src
ADD package.json /app/package.json
ADD package-lock.json /app/package-lock.json
ADD tsconfig.json /app/tsconfig.json

WORKDIR /app

RUN set -x \
  && npm ci \
  && npm run build \
  && npm prune --production

FROM node:10.15.3-alpine

ARG EXPOSED_PORT=3000
ENV PORT=${EXPOSED_PORT}

COPY --from=builder /app/node_modules /app/node_modules
COPY --from=builder /app/dist /app/dist

RUN chown -R node:node /app

WORKDIR /app

EXPOSE ${EXPOSED_PORT}

USER node

CMD ["node", "dist/server.js"]