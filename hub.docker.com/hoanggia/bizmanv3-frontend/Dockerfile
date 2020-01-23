# build environment
FROM node:10.15.1-alpine as build
WORKDIR /app
RUN npm install -g yarn
ENV REACT_APP_API_HOST http://167.71.204.250:3000
ENV PATH /app/node_modules/.bin:$PATH
COPY package.json /app/package.json
COPY . /app
RUN yarn install && yarn build

# production environment
FROM nginx:1.16.0-alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
# CMD ["nginx", "-g", "daemon off;"]