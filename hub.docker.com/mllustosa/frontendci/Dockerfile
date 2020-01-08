FROM frolvlad/alpine-glibc:alpine-3.9_glibc-2.29

## Dependencies that need to stay in the image
RUN apk update \
  && apk add --no-cache bash \
  python \
  py-pip \
  git

# Install system dependencies for image creation that will get removed later
RUN apk update \
  && apk add --no-cache --virtual build-deps \
  make \
  gcc \
  libffi-dev \
  openssl-dev \
  python-dev \
  build-base

# Update pip
RUN pip install --no-cache --upgrade pip

# Install requests (Needed for azure-client)
RUN pip install --no-cache requests

# Upgrade setup tools (Needer for azure-client)
RUN pip install --no-cache --upgrade setuptools

# Install azure-cli
RUN pip install --no-cache azure-cli

# Install node and npm
RUN apk add --no-cache nodejs nodejs-npm

# Remove unneeded dependencies and folders
RUN apk del build-deps \
  && rm -rf /var/cache/apk/*