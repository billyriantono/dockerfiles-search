FROM node:alpine

# Work directory
WORKDIR /usr/src/app

# Default ENV
ENV NODE_ENV=production

# Install bash, missing on alpine.
RUN apk update && apk add bash

USER node

# Default command
CMD ["npm", "start"]
