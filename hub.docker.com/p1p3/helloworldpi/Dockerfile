
# use our prepared Raspberry Pi compatible Docker base image with Node.js
FROM hypriot/rpi-node:latest

# Copy project files and change working directory
COPY ./src /src
WORKDIR /src

# Expose container port
ENV PORT=80
EXPOSE $PORT

# Install npm dependencies and run application
# RUN npm install
# CMD node app.js