FROM keymetrics/pm2:10-alpine

# Install git (required on Alpine for some dependencies)
RUN apk add --update --no-cache git

# Setup
WORKDIR /home/node/app
RUN chown -R node:node /home/node/app
USER node

# Dependencies
COPY package*.json ./
RUN npm install --only=prod --no-optional

# Copy files
COPY --chown=node:node ./ ./

# Start bot
CMD ["pm2-runtime", "index.js", "--name=VoiceLogger"]
