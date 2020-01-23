FROM node:10-alpine

LABEL AUTHOR="Bruno Correia <bruno.correia@leads2b.com>"

WORKDIR /app

ARG NODE_ENV=production

# Prepare and install dependencies
COPY package.json yarn.lock ./
RUN yarn install

# Copying the application
COPY . .

CMD ["yarn", "start"]
