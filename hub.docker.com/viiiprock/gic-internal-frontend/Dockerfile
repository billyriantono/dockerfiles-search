FROM node:alpine

# If use yarn `RUN npm config set scripts-prepend-node-path true`
RUN npm config set scripts-prepend-node-path true
# Cache the files
ADD package.json yarn.lock /tmp/frontend/

# Set working dir
RUN mkdir -p ./usr/src/frontend
WORKDIR /usr/src/frontend

# Copy package json files for services
COPY package.json yarn.lock ./
RUN yarn install --silent

COPY . ./
RUN yarn build

EXPOSE 3000
CMD ["yarn", "start:staging"]