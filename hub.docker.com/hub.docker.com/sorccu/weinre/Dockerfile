FROM sorccu/node:0.10
MAINTAINER Simo Kinnunen

# Install weinre
RUN npm install -g weinre

# Expose default port
EXPOSE 3333

# Default command
CMD ["/usr/local/bin/weinre", "--httpPort", "3333", "--boundHost", "0.0.0.0"]
