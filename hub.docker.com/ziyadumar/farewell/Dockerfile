FROM node:11.15.0-alpine AS angular

WORKDIR /app
EXPOSE 80

ARG angular_conf=production
RUN echo "Environment: ${angular_conf}"
WORKDIR /app
COPY . .
RUN npm install 
RUN npm i npm@latest -g
RUN npm rebuild node-sass
RUN ./node_modules/.bin/ng build --configuration ${angular_conf}

FROM nginx:alpine

COPY --from=angular /app/dist/farewell/ /usr/share/nginx/html/