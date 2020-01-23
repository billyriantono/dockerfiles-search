FROM node:12.14.1-alpine as build-step
WORKDIR /app
COPY package.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx:1.17.7-alpine as prod-stage
COPY --from=build-step /app/dist/family-budget /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]