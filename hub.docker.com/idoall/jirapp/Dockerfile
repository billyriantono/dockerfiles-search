FROM node:12.13-alpine as build

WORKDIR /app

COPY package*.json ./
RUN npm install --silent

COPY . .
RUN npm run build -- --prod

FROM nginx:alpine as runtime

COPY nginx.conf /etc/nginx/nginx.conf

COPY --from=build /app/dist/ /usr/share/nginx/html/