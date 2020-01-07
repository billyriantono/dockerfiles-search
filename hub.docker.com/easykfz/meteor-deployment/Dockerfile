FROM ezprint/meteor-deployment:1.4

MAINTAINER Daniel Holzmann <d@velopment.at>

RUN DEBIAN_FRONTEND=noninteractive apt-get update \
    && apt-get install -y --no-install-recommends \
        libcairo2-dev libjpeg8-dev libpango1.0-dev libgif-dev build-essential g++ \
    && rm -rf /var/lib/apt/lists/*