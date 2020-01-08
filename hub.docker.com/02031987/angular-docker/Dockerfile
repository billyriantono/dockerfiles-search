FROM node:8.15.0-alpine as build
WORKDIR /app
COPY package*.json /app/
RUN npm i
COPY ./ /app/
ARG configuration=production
RUN npm run build -- --output-path=./dist/my --configuration $configuration
# Part 2
FROM nginx:alpine as final
EXPOSE 80
EXPOSE 443
COPY --from=build /app/dist/my/ /usr/share/nginx/html
COPY ./nginx.conf /etc/nginx/conf.d/default.conf