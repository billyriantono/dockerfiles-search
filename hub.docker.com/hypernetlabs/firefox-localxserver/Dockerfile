FROM ubuntu:latest

# Update apt, install some stuff, and remove the apt lists to reduce the package size
RUN apt-get update && apt-get install -y \
    firefox \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

ENTRYPOINT ["firefox"]