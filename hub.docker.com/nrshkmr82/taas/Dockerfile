#Stage 1
FROM node:11.8.0-alpine as node

WORKDIR /app
COPY . .

RUN npm install
RUN npm rebuild node-sass
RUN npm run build --prod


#Stage 2
FROM nginx:alpine
COPY nginx.conf /etc/nginx/nginx.conf
COPY --from=node /app/dist/Taas /usr/share/nginx/html

