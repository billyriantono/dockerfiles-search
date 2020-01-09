# Do the npm install or yarn install in the full image
FROM mhart/alpine-node:10 as BUILDER

WORKDIR /app

COPY . .

RUN npm install && npm run build:prod

RUN rm -rf node_modules && npm install --production

# Amd then copy over node_modules, etc from that stage to the smaller base image
FROM mhart/alpine-node:base-10

WORKDIR /app
COPY --from=BUILDER /app .

EXPOSE 5000
CMD ["node", "server.js"]
