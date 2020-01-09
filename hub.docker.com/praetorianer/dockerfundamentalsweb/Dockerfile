FROM node:8.2

# Make api port configurable
# Optional (if not configured in docker-compose.yml file)
# ENV PORT=8080
# ENV API_HOST="api:5000"
# ENV DEBUG="ldv:server,worker"
# ENV NODE_ENV="production"

# Create app directory
WORKDIR /opt/web

# Bundle app source
COPY . .

# Install app dependencies
RUN npm install

CMD [ "npm", "start" ]
