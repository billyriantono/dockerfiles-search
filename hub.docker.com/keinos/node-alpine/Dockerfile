FROM mhart/alpine-node:latest as build
RUN apk update && \
  apk add --no-cache binutils && \
  strip /usr/bin/node

FROM keinos/alpine:latest
COPY --from=build /usr/bin/node /usr/bin/
COPY --from=build /usr/lib/libgcc* /usr/lib/libstdc* /usr/lib/
