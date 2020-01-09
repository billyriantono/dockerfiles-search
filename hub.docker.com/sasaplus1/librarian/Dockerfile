FROM alpine:latest

WORKDIR /root

RUN apk --no-cache add bash nodejs yarn

COPY . .

RUN yarn install --frozen-lockfile

ENTRYPOINT ["yarn", "build"]
