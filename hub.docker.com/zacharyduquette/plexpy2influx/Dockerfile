FROM mhart/alpine-node:4
WORKDIR /app
COPY package.json ./
RUN npm install --production

FROM mhart/alpine-node:base-4
WORKDIR /app
COPY --from=0 /app .
COPY . .
CMD [ "node", "app.js" ]