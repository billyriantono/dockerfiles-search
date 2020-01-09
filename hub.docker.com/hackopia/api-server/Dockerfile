FROM node:8.7.0-alpine

# Set a working directory
WORKDIR /usr/src/app

# Copy application files
COPY . .

# Install dependencies
RUN apk add --no-cache libsodium && \
  yarn install --production --no-progress && \
  yarn cache clean

# Run the container under "node" user by default
USER node

EXPOSE 8001

CMD [ "node", "build/server.js" ]
