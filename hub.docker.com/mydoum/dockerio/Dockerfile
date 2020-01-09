# Dockerfile
# The FROM directive sets the Base Image for subsequent instructions
FROM node:alpine

# Install needed deps and clean up after
RUN apk update
RUN apk add --no-cache \
  git \
  python \
  make \
  gcc \
  g++

# Set the work directory
RUN mkdir -p /var/www/

# To get the repository without SSH key , it uses an API key available on
# bitbucket->freshio->settings->API key
RUN cd /var/www; git clone https://freshio:ikxDKWYKN95y4sXoKggsL6XYCBBioDbN@bitbucket.org/freshio/backend.git

# Launching the application
WORKDIR /var/www/backend

# Installing the application
RUN npm install

# Entrypoint
CMD ["node_modules/.bin/gulp", "docker"]

#Expose the port
EXPOSE 3000

