FROM mongo:4.2.0
RUN apt-get update \
    && apt-get install -y --no-install-recommends s3cmd \
    && rm -rf /var/lib/apt/lists/*