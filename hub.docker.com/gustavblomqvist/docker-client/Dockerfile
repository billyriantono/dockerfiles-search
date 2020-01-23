### BUILD CLIENT ###

# Import Node.js
FROM node:latest as node

WORKDIR /build

COPY /Client .
COPY /nginx.conf .

# Install packages
RUN npm ci

# Build Project
RUN npm run build

### WEB SERVER ###

# Import nginx
FROM nginx:alpine

COPY --from=node /build/dist/Client /usr/share/nginx/html
COPY --from=node /build/nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80