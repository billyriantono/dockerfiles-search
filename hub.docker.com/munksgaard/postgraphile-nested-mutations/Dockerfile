FROM node:alpine
LABEL description="Instant high-performance GraphQL API for your PostgreSQL database https://github.com/graphile/postgraphile"

WORKDIR /project

COPY package.json .
COPY package-lock.json .

RUN npm install

EXPOSE 5000
ENTRYPOINT ["/project/node_modules/.bin/postgraphile", "-n", "0.0.0.0"]
