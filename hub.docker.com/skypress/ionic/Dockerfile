FROM node:12-alpine

# Create Working Directory
RUN mkdir -p /app && \
  chown node:node /app

# Set Working Directory
WORKDIR /app

# Install ionic globally
RUN su node && \
  npm install -g ionic

# Use the node user
USER node
