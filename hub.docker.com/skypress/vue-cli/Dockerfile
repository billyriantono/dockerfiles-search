FROM skypress/npx:latest

# Switch to root user
USER root

# Install Vue CLI and Service
RUN yarn global add @vue/cli @vue/cli-service-global

# Use the "node" user
USER node

# Expose Ports
EXPOSE 8080
