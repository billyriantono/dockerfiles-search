FROM node:10-alpine as builder

ENV NODE 10
ENV PLATFORM alpine
ENV ARCH x64

WORKDIR /app

# Extra tools for native dependencies
RUN apk add --no-cache make gcc g++ python

# Only copy package files (npm ci will only run when they have changed)
COPY package* ./
RUN npm ci

# Only copy files needed for building
COPY tsconfig.json .
COPY src src
RUN npx @zeit/ncc build --no-cache src/main.ts --out dist
RUN npx pkg --public --target node${NODE}-${PLATFORM}-${ARCH} --output dist/personal-metrics dist/index.js

FROM node:10-alpine
EXPOSE 9000
COPY --from=builder /app/dist/personal-metrics .
CMD ["./personal-metrics"]
