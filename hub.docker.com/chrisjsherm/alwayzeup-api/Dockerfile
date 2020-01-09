FROM node:12.11.1-slim

# Install dumb-init for easier signal handling of SIGINT/SIGTERM/SIGKILL.
RUN wget https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_1.2.0_amd64.deb
RUN dpkg -i dumb-init_*.deb
ENTRYPOINT ["dumb-init"]

COPY package*.json ./
RUN npm install --prod

COPY . ./

# Override at build time with:
# `docker build --build-arg DATABASE_CONNECTION_STRING=mongodb://@mongodb:27017/websites # ... rest of command
ARG DATABASE_CONNECTION_STRING=mongodb://@localhost:27017/websites

# Set environment variable to argument value.
ENV DATABASE_CONNECTION_STRING=${DATABASE_CONNECTION_STRING}

EXPOSE 8080

# Node images provide the unprivileged `node` user to avoid
# security issues with running as root inside the container.
USER node

# Start the node process.
CMD [ "/usr/local/bin/node", "./src/index.js" ]
