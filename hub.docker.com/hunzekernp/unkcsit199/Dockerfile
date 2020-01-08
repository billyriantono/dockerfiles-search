#Gets a base image(debian)
FROM debian:latest

#Enviroment Variable for this dockerfile
ENV S6_RELEASE 1.21.4.0

#S6 Overlay(process supervisor)
ADD https://github.com/just-containers/s6-overlay/releases/download/v$S6_RELEASE/s6-overlay-amd64.tar.gz /tmp/
RUN tar xzf /tmp/s6-overlay-amd64.tar.gz -C /

#Installs htop for practice
RUN apt-get update
RUN apt-get install cowsay fortune -y

# Copy the install script into the container to be executed on startup
COPY install.sh /etc/cont-init.d/
RUN chmod u+x /etc/cont-init.d/install.sh

ENTRYPOINT ["/init"]
