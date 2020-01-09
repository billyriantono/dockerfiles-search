FROM ghost:0.9.0
RUN set -x \
    && npm install ghost-cloudinary-store \
    && mkdir content/storage \
    && cp -r node_modules/ghost-cloudinary-store content/storage/ghost-cloudinary-store \
    && apt-get update -qq \
    && apt-get install -y --no-install-recommends \
         dnsutils \
         netcat \
    && rm -rf /var/lib/apt/lists/*
COPY ./config.js /var/lib/ghost/config.js
HEALTHCHECK --interval=5s --timeout=5s CMD curl --fail http://localhost:2368/ || exit 1
