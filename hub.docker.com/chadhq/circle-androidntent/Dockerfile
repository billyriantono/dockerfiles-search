from node:alpine
WORKDIR /app
ADD . /app
RUN yarn install
RUN npm run build
ENTRYPOINT ["npm", "run", "prod"]
