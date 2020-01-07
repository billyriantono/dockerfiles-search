FROM nginx:latest
MAINTAINER Marco Monteiro <marco@neniu.org>

RUN echo "\nstream {\n    include /etc/nginx/stream.d/*.conf;\n}\n" >> /etc/nginx/nginx.conf && \
    mkdir /etc/nginx/stream.d
