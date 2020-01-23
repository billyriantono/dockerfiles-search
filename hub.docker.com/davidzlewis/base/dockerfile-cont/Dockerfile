FROM debian:latest

# Install necessary packages.
RUN apt-get update && apt-get install -y gimp \
    && rm -rf /var/lib/apt/lists/*

CMD [ "gimp" ]