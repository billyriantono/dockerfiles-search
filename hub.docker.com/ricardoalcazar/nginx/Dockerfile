##
# NGINX configuration with Jenkins
# Modified: R. Alcazar 8/17/2018
##

FROM nginx:latest

LABEL maintainer=ricardo.d.alcazar@gmail.com

# Update with the latest OS patches
RUN apt-get update && apt-get upgrade -y

# Update the configuration files
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 80
CMD ["nginx"]




