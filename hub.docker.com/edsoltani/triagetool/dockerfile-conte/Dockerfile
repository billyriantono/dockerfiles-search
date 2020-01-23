############################################################
# Dockerfile to build Nginx Installed Containers
# Based on alpine
############################################################


# Set the base image to Alpine
FROM nginx:alpine

COPY WebContent /usr/share/nginx/html

# Expose ports
EXPOSE 80

# Set the default command to execute
# when creating a new container
CMD ["nginx", "-g", "daemon off;"]
