FROM nginx:alpine

LABEL maintainer="Paulino Padial <github.com/ppadial>"

# Remove default files that we don't need
RUN rm /etc/nginx/nginx.conf
RUN rm /etc/nginx/conf.d/*.conf
RUN rm /etc/nginx/*.default

# Copy to override configurations
COPY nginx.conf /etc/nginx/nginx.conf
