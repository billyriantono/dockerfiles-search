# Base image
FROM node:12

# Set working directory
RUN mkdir /app
WORKDIR /app

# Add `/app/node_modules/.bin` to $PATH
ENV PATH /app/node_modules/.bin:$PATH

# Install awscli
RUN apt-get update && apt-get install -yq awscli
