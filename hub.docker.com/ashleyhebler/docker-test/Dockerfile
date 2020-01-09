FROM node:lts-alpine

RUN apk add --no-cache git

# Copy the package.json and package-lock.json
COPY package*.json ./

# Copy yarn lock if present
COPY *.lock ./


# Copy tasks - folder of task functions
COPY entrypoint.js ./

# Install dependencies
RUN npm install

# Run `node entrypoint.js`
ENTRYPOINT ["node", "entrypoint.js"]