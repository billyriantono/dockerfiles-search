### STAGE 1: Build ###
FROM node:alpine AS build

WORKDIR /usr/src/app
COPY package.json ./
RUN npm install

COPY . .
RUN npm run-script build

### STAGE 2: Run ###
FROM nginx:alpine
COPY --from=build /usr/src/app/dist/frontend /usr/share/nginx/html
