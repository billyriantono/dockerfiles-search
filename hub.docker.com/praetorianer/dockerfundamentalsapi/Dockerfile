FROM node:8.2

# Make api port configurable
# Optional: Only needed if not configured in docker-compose.yml file
# ENV PORT=5000
# ENV DB="postgres://postgres:sup3rsecure@postgres/awesomeapp'"
# ENV DEBUG="ldv:server,worker"
# ENV NODE_ENV="production"

# Create app directory
WORKDIR /opt/api

# Bundle app source
COPY . .

# Install app dependencies
RUN npm install

# Optional: Only needed if not exposed in docker-compose.yml file
EXPOSE $PORT

CMD [ "npm", "start" ]
