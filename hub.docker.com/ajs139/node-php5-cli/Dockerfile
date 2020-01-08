FROM node:6.10.3
MAINTAINER Andrew Stephens <ajs139@gmail.com>

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
      build-essential \
      jq \
      php5-cli \
      libcairo2-dev \
      libgif-dev \
      libjpeg62-turbo-dev \
      libpango1.0-dev \
      python-dev \
      python-pip && \
    rm -rf /var/lib/apt/lists/*

RUN pip install --upgrade pip && \
    pip install awscli

RUN echo "US/Eastern" > /etc/timezone && \
    dpkg-reconfigure -f noninteractive tzdata
CMD ["php", "-a"]
