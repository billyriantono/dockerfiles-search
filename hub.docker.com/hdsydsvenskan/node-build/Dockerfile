FROM node:8

# Install jq and rsync
RUN apt-get update \
    && apt-get install -y --no-install-recommends jq rsync build-essential \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

ENV NODE_ENV development
CMD ["yarn", "install"]
