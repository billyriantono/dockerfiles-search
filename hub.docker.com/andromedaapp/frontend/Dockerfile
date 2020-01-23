FROM node AS builder
MAINTAINER Giambra Domenico <zorinik@gmail.com>

COPY . /app

WORKDIR /app
RUN npm ci
RUN $(npm bin)/ng build --prod

####################################

FROM nginx:alpine
COPY nginx.conf /etc/nginx/conf.d/default.conf
RUN rm -rf /usr/share/nginx/html/*
COPY --from=builder /app/dist/andromeda-frontend /usr/share/nginx/html
EXPOSE 80
EXPOSE 443
ENTRYPOINT ["nginx", "-g", "daemon off;"]
