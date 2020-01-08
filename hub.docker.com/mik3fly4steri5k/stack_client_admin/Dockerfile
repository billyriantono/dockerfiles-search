# This image will be based on the official Nginx docker image
# to serve static contents
FROM nginx
MAINTAINER Bryan MARTIN <martinbryan.eu@gmail.com>

# We copy over our build to the Nginx server
COPY build/production/Admin /usr/share/nginx/html

# Tell Docker we are going to use this port
EXPOSE 80