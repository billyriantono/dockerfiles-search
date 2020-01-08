FROM debian

# Install base tools
RUN apt-get update && \
    apt-get install -y build-essential curl git python-dev python-pip python-virtualenv supervisor vim wget && \
    rm -rf /var/lib/apt/lists
