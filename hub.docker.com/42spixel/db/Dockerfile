FROM postgres:11

# Metadata
LABEL mantainer="Gius. Camerlingo <gcamerli@gmail.com>"
LABEL version="1.0"
LABEL description="Postgres db for Docker."

# Docker image name
ENV NAME=db

# Timezone
ENV TZ="Europe/Paris"

# Update system and install packages
RUN apt-get update
RUN apt-get install -y iputils-ping --no-install-recommends

# Clean system
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# User
RUN useradd -ms /bin/bash spixel

# Home
ENV HOME=/home/spixel

# Permissions
RUN chown -R spixel:spixel $HOME

# Healthcheck
COPY healthcheck /usr/local/bin/
RUN chmod 744 /usr/local/bin/healthcheck

# Change user
USER spixel
