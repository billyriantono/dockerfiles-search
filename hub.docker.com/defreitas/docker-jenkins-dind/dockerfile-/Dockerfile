# Do the npm install or yarn install in the full image
FROM mhart/alpine-node:8
WORKDIR /app
#COPY package.json yarn.lock ./
COPY . .
RUN yarn install --production


# And then copy over node_modules, etc from that stage to the smaller base image
FROM mhart/alpine-node:base-8
WORKDIR /app
COPY --from=0 /app .
COPY . .
EXPOSE 3000
CMD ["node", "index.js"]