FROM node:latest

# Create the directory!
RUN mkdir -p /user/src/bot
WORKDIR /user/src/bot

# Copy and Install our bot
COPY package.json /user/src/bot
RUN npm install
RUN npm update

# Our precious bot
COPY . /usr/src/bot

# Start me!
CMD ["node", "index.js"]