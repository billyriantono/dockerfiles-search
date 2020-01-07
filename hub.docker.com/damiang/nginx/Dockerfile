FROM nginx:latest

COPY nginx.conf /etc/nginx/nginx.conf
COPY sites-enabled/default.conf /etc/nginx/conf.d/default.conf
COPY includes /etc/nginx/includes

COPY ssl/cert.pem /etc/nginx/ssl/cert.pem
COPY ssl/cert.key /etc/nginx/ssl/cert.key