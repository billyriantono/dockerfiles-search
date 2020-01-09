FROM python:3.6-stretch

RUN DEBIAN_FRONTEND=noninteractive apt-get update \
    && apt-get install -y --no-install-recommends \
      apt-transport-https \
      ca-certificates \
      curl \
      gnupg \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN pip install pipenv pytest wheel twine
