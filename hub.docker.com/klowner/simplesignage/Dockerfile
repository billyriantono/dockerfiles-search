FROM node:alpine
WORKDIR /app
COPY . /app
RUN npm i && npm run build

FROM node:alpine
WORKDIR /app
COPY package.json package-lock.json .* ./
COPY --from=0 /app/dist dist
RUN npm i --production
EXPOSE 3000
VOLUME /app/media
CMD ["npm", "start"]
