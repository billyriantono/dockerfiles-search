FROM node:12-alpine

RUN apk add --no-cache tzdata
# for image generation
RUN apk add --no-cache \
    build-base \
    g++ \
    cairo-dev \
    jpeg-dev \
    pango-dev \
    giflib-dev

ONBUILD ARG NODE_ENV=development

RUN mkdir -p /usr/app
WORKDIR /usr/app

ONBUILD COPY --from=installer /usr/app/node_modules ./node_modules
ONBUILD COPY --from=builder /usr/app/lib ./lib
ONBUILD COPY package.json yarn.lock ./

ONBUILD COPY src ./src
ONBUILD COPY data ./data
ONBUILD COPY fonts /usr/share/fonts/
ONBUILD RUN sh -c "if [ \"$NODE_ENV\" == \"production\" ]; then rm -rf src; fi"
ONBUILD ENV NODE_ENV=${NODE_ENV}

CMD ["yarn", "serve"]
