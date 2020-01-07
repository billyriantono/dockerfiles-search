FROM node:8 as build
WORKDIR /app
COPY ./package.json ./package-lock.json ./
RUN npm install
COPY . .
RUN npm run build

FROM node:8-slim
WORKDIR /app
COPY --from=build /app/package.json /app/dist/ /app/node_modules/ ./
EXPOSE 3000
CMD ["npm","start"]