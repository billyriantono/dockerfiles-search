FROM node:alpine

# Install dependencies via apk
RUN apk update && apk upgrade \
    && apk add --no-cache python  g++ make \
    && rm -rf /var/cache/apk/*

# Install zero globally
RUN npm install --quiet --no-progress --unsafe-perm -g zero

# Run zero in production mode
ENV NODE_ENV production

# Expose port
ENV PORT 80
EXPOSE 80

WORKDIR /app

CMD ["zero"]
