# Credit: https://medium.com/@shakyShane/lets-talk-about-docker-artifacts-27454560384f
# Stage 1 - build
FROM node:latest AS build-deps
WORKDIR /usr/src/app
COPY package.json package-lock.json ./
ENV CI true
RUN npm install
COPY . ./
RUN npm test
RUN npm run build

# Stage 2 - production
FROM nginx:1.14-alpine
COPY --from=build-deps /usr/src/app/build /usr/share/nginx/html
EXPOSE 80
CMD [ "nginx", "-g", "daemon off;" ]