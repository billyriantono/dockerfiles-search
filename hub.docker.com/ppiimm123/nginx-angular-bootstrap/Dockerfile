FROM nginx:1.17.5-alpine

# Copy the angular nginx config
COPY default.conf /etc/nginx/conf.d/

# Remove default nginx website
RUN rm -rf /usr/share/nginx/html/*
