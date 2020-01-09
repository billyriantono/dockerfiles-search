# Base image
FROM nginx:latest

COPY index.html /usr/share/nginx/html
COPY appspec.yml /usr/share/nginx/html
COPY LICENSE.txt /usr/share/nginx/html
COPY scripts /usr/usr/share/nginx/html

#Which port to use?
EXPOSE 80
