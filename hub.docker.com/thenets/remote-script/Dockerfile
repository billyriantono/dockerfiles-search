FROM ubuntu:16.04

# Install upgrades
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get autoremove -y

# Install curl
RUN apt-get update && \
    apt-get install -y curl
    
# Set entrypoint file
ADD /entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT [ "/entrypoint.sh" ]
