FROM ubuntu:16.04

# Install dependencies
RUN apt-get update && apt-get install -y openssl

# certificate
VOLUME ["/certificate"]

# Keep docker running
CMD tail -f /dev/null