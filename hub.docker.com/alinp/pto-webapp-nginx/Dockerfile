# Dockerfile-nginx

# Docker for UI build
FROM node:10.9 as angular_build
# Install angular
RUN npm install -g @angular/cli
RUN mkdir /app
WORKDIR /app
# Copy ui files
COPY ui/ .
# Build ui
RUN npm install
RUN ng build --prod

# Web server for UI and reverse proxy for MW (nginx)
FROM nginx:1.15.8 as nginx_run

RUN apt update
RUN apt install openssl
RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/nginx-selfsigned.key -out /etc/ssl/certs/nginx-selfsigned.crt -subj "/C=NL/ST=Zuid Holland/L=Rotterdam/O=Sparkling Network/OU=IT Department/CN=ssl.raymii.org"

# Nginx will listen on this port
EXPOSE 80
# Remove the default config file that
# /etc/nginx/nginx.conf includes
RUN rm /etc/nginx/conf.d/default.conf
# Copy nginx condig file
COPY app.conf /etc/nginx/conf.d
# Copy builded angular app
COPY --from=angular_build /app/dist/ .