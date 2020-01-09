FROM node:11

# Create app directory
WORKDIR /app

# Copy the package and yarn.lock to workdir
COPY package.json /app
COPY yarn.lock /app

# Install unglue-server
RUN yarn install

# Start server when docker image launches
CMD ["yarn", "start"]

# Expose server port 3000
EXPOSE 3000