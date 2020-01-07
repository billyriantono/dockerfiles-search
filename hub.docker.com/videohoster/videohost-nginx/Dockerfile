FROM nginx:latest

# Remove default nginx configs.
RUN rm -f /etc/nginx/conf.d/*
RUN rm -f /etc/nginx/nginx.conf

# Add configuration files
COPY conf/nginx.conf /etc/nginx/nginx.conf
COPY conf/nginx.video.conf /etc/nginx/conf.d/video.conf
COPY crt/mykey.key /etc/nginx/crt/private.key
COPY crt/cert.crt /etc/nginx/crt/public.crt

EXPOSE 80
