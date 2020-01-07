FROM alpine:3.6
MAINTAINER Julio Lustosa "contato@juliolustosa.com.br"

# Set an environment variable
ENV USER deploy

# Update and upgrade packages
RUN apk update && apk upgrade

# Install packages
RUN apk add --no-cache \
  bash \
  curl \
  tzdata

# Copy scripts
RUN mkdir /build-scripts
COPY ./build-scripts /build-scripts
RUN chmod +x /build-scripts/*.sh

# Add new user
RUN /build-scripts/add-user.sh

# Clear all
RUN /build-scripts/clear.sh

# Set new user
USER $USER

# Set workdir
WORKDIR /home/$USER